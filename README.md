# TCR (Test && Commit || Revert) utility for C#
Before we start, all the credits goes to [Murex](https://github.com/murex). 
This utility is based on [their implementation](https://github.com/murex/Kata-BowlingGame).
I'd like to thank them for their incredible work.
Feel free to check theirs repos and I'd recommend you attend one of their workshops.

All I did was focusing on the C# language and make it easy to be integrated in a solution.

So I won't be explaining how the utility works as I didn't modify the internals. 
If you'd like to know how to use it, feel free to check [their documentation](https://github.com/murex/Kata-BowlingGame/blob/master/tcr/TCR.md).
I will focused on what makes this one specific and how to integrate it in a solution.

## Licence

[Here](LICENSE.md)'s the licence file, from [Murex](https://github.com/murex). 

## Toolchain selection
The script can support multiple toolchains. 
I mainly focused on being compatible with main test frameworks.

| Toolchain | Test Framework | Default |
|-----------|---------------|--------|
| mstest    | MsTest        | &check;|
| nunit     | NUnit         |        |
| xunit     | xUnit         |        |

You do not have to install anything in order to use them. They are just variations of the `dotnet build` and `dotnet test` commands.

In order to select a specific toolchain, you will have to use the toolchain option `-t` with the name of the toolchain.
For example, running the utility using the default toolchain (MsTest) requires this command: `./tcrw`,  while using a specific toolchain (xUnit) requires this one: `./tcrw -t xunit`.

## Outside-in approach compliance
TCR can be a problem if you're willing to follow the TDD Double-loop as the feature you're implementing will be failing for a while. Actually, until it's implemented...

Out-of-the-box, TCR won't let you as your acceptance project will tested too so your changes will be reverted. But I'm proposing a solution: mark the feature under development with the `InProgress` category until it's finished. This will prevent those tests to be monitored.

Here's the filter used on the test command (the name of the filter may vary depending on the test framework): `Category!=InProgress`

It also means it's up to you to change it if you already have different guidelines, or if you want to expand the filter. All you have to do is updating the [toolchain file](tcr/tcr_shell/toolchains) for a specific test framework.

## Integration
This is the easy part: just copy at the same level than src|tests folders both [tcr folder](tcr) and [watcher script](tcrw).

This is it. Then run the script and have fun!