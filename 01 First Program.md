---
slug: 01-first-program
date: 2021-03-21
---

# First Program

I came across[^osl] the [memstate](https://github.com/DevrexLabs/memstate) library (after reading about CQRS and eventsourcedb), which seemed very similar to `acid-state` on Haskell world, but based on CQRS and in the dotnet world. This would be a perfect candidate for the [[Baseline]] project, and as a replacement of LiteDB. 

There were *no* examples for it in F#, however. So I bootstrapped a new dotnet console project and decided to get something working by referencing memstate's tests.

[Program.fs](https://github.com/srid/OneBird/blob/083cab366db6d1c5a3f8b1b595576d6f65772940/Program.fs):

```fsharp
// Learn more about F# at http://docs.microsoft.com/dotnet/fsharp

open System
open Memstate
open Memstate.JsonNet

type Tweet =
    { Id: int
      Message: string
    }

type TwitterModel() =
    let mutable tweets: Tweet list = []

    member this.Tweets = tweets

    member this.PostTweet(msg: string) = 
        let tweet = { Tweet.Id = 1; Message = msg }
        tweets <- tweets @ [tweet]
        tweet
        

// Events 

type Tweeted(tweet: Tweet) =
    inherit Event()

// Commands

type PostTweet(msg: string) = 
    inherit Command<TwitterModel, int>()

    member this.Msg: string = msg
    
    override Command.Execute(model: TwitterModel): int =
        let tweet = model.PostTweet msg
        Command.RaiseEvent (new Tweeted(tweet))
        tweet.Id

// Query

type AllTweets() =
    inherit Query<TwitterModel, Tweet list>()

    override Query.Execute(model: TwitterModel) =
        model.Tweets

[<EntryPoint>]
let main argv =
    // TODO: understand concepts used
    printfn "Begin"
    async {
        let! engine = Engine.Start<TwitterModel>() |> Async.AwaitTask
        let cmd = new PostTweet("Hello world")
        let! res = engine.Execute(cmd) |> Async.AwaitTask
        printfn "res: %d" res
        let query = new AllTweets()
        let! allTweets = engine.Execute(query) |> Async.AwaitTask
        printfn "%A" allTweets
        printfn "Fin."
    } |> Async.RunSynchronously
    0 // return an integer exit code
```

Keep in mind that this is the first F# code I wrote, and I did that without actually formally studying the language ahead. There is a TODO in there as a reminder for myself to study the concurrency topic (the async stuff). Microsoft has pretty good [introductory docs](https://docs.microsoft.com/en-us/dotnet/fsharp/tutorials/asynchronous-and-concurrent-programming/async?source=docs) on it.

<script src="https://utteranc.es/client.js"
        repo="srid/learning-fsharp"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

## Links

- [r/fsharp post](https://www.reddit.com/r/fsharp/comments/mablsh/memstate_inmemory_eventsourced_acidtransactional/)

[^osl]: https://opensourcelibs.com/libs/eventstore
