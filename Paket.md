To begin with, use plain dotnet project templates using NuGet. Overtime, *when necessary*, switch to the [Paket](https://fsprojects.github.io/Paket/) dependency manager.

For eg., when I found the need to use a Git fork of a library, I chose to use Paket - as it allows [Git dependencies](http://fsprojects.github.io/Paket/git-dependencies.html). **EDIT**: I was wrong; Paket's git support is *extremely* lack.

Note that #[[MiniScaffold]] uses Paket.

## External links

- [First change](https://github.com/srid/Feather/pull/4) to migrate from NuGet to Paket.