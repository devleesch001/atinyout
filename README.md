# atinyout

`atinyout` is a lightweight AT command wrapper and an alternative to `atinout`. It sends AT commands to a modem via `socat` and returns clean, script-ready data without extraneous terminal echoing or carriage returns.

## Features

- **Lightweight**: Minimal dependencies, simply a shell script leveraging `socat`, `awk`, `tr`, and `grep`.
- **Clean output**: Parses standard AT responses, strips noise like carriage returns (`\r`), and provides only the relevant data.
- **Error handling**: Detects modem `ERROR` responses and reports them clearly.
- **Raw mode**: Allows viewing the direct, unparsed response from the modem for debugging.
- **Easy Configuration**: Quickly configurable via environment variables.

## Requirements

- POSIX-compliant shell (`sh`)
- `socat`
- Standard UNIX utilities: `awk`, `tr`, `grep`

## Installation

You can simply download the `atinyout` script and make it executable:

```bash
chmod +x atinyout
```

(Optional) Place it in your `PATH` for global access (e.g., `/usr/local/bin`):

```bash
sudo cp atinyout /usr/local/bin/
```

## Usage

```text
Usage: atinyout [OPTIONS] <AT_Command>

    Options:
      -h, --help    Show help message and exit
      -r, --raw     Show the raw response from the modem
```

### Examples

Send a basic AT command (e.g. to check the CCID):
```bash
atinyout AT+CCID
```

Send a command and view the raw response (includes the command echo, carriage returns, and `OK` terminator):
```bash
atinyout -r AT+CGSN
```
or
```bash
atinyout --raw AT+CIMI
```

## Configuration

You can configure `atinyout` using environment variables. The script uses the following variables along with their default values:

- `PORT` (default: `/dev/ttyUSB2`): The serial port your modem is connected to.
- `BAUD` (default: `115200`): The baud rate for the serial connection.
- `TIMEOUT` (default: `2`): The timeout in seconds for the modem to respond.

### Configuration Examples

To override the default port and baud rate for a single command:
```bash
PORT=/dev/ttyUSB0 BAUD=9600 atinyout AT+CSQ
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
Copyright (c) 2026 Alexis DEVLEESCHAUWER
