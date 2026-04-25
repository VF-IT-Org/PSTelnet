# PSTelnet

PowerShell telnet scripts for querying remote devices and returning PRTG-friendly numeric output.

## Scripts

| Script | Purpose |
| --- | --- |
| `PSPower.ps1` | Connects over telnet, runs a remote command, and returns a scaled current/power value. |
| `TelnetMFIcatvcalue.ps1` | Connects over telnet, runs a remote command, and returns a temperature-style value converted to Fahrenheit. |

## Requirements

- PowerShell 5.1 or later
- Network reachability to the target telnet host
- Valid telnet credentials for the device
- A device command that returns the expected numeric value format

## Usage

Example:

```powershell
powershell -ExecutionPolicy Bypass -File .\PSPower.ps1 -RemoteHost "192.168.0.55" -user "username" -pass "password" -catlocation "cat /proc/analog/rms2"
```

Both scripts:

1. Open a TCP connection to the target host on port 23 by default.
2. Send the username, password, and command after short waits.
3. Read the device response.
4. Parse the line after the echoed `cat /proc/...` command and emit a value string suitable for monitoring.

## Maintenance notes

- Credentials are currently passed directly as script parameters.
- The scripts assume a very specific remote prompt and response format.
- A future hardening pass should add connection error handling, timeouts, and reusable shared telnet logic.
