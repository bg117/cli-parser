# cli-parser

Getopt but for C#.

## Installation

Simply copy the CommandLineParser.cs file onto your project. All objects are in `namespace CliParser`.

## Usage

To use `cli-parser`, specify an array of `CommandLineOption` and the command string array to parse (usually `string[] args` in `Main`). Then, pass an `Action<string, string[]>` which receives the current option being parsed and its corresponding arguments.

## Example

```csharp
using CliParser;

CommandLineOption[] opts = new []
{
  new []
  {
    Option = "help",
    IsLongOption = true,
    RequiresArgument = false
  },
  new []
  {
    Option = "test",
    IsLongOption = true,
    RequiresArgument = true
  },
  new []
  {
    Option = "b",
    IsLongOption = false,
    RequiresArgument = false
  }
};

CommandLineHelpers.ParseCommandLine(opts, args, (opt, arg) =>
{
  switch (opt)
  {
    case "help":
      Console.WriteLine("--help passed");
      break;
    case "test":
      Console.WriteLine("--test passed with args: {0}", string.Join(",", arg));
      break;
    case "b":
      Console.WriteLine("-b passed");
      break;
  }
}
```

This example program will print `--help passed` when --help is passed, `-b passed` when -b is passed, and `--test passed with args: <csv-args>` when --test is passed with an argument (multiple --test options can be passed).
