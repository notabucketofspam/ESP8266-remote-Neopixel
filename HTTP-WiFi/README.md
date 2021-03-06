# HTTP-WiFi

Making / flashing the SPIFFS image:

- First time:
  - `./makemkspiffs.sh`
  - `make erase_flash`
- After any time `make erase_flash` is executed:
  - `make flash`
  - Wait for SPIFFS to finish formatting
  - `./flashspiffs.sh`
- Any other time:
  - `make app-flash`

Other notes:

- If using a static IP, set `tcpip adapter -> IP Address lost time interval (seconds)` in menuconfig to zero. This should've been something that's dealt with in the code, but order of operations in the preprocessor seems to negate it.
- For whatever reason, `esp_wifi_connect()` often hangs with the message `wifi:state: 0 -> 2 (b0)`. The task watchdog will subsequently restart the module and (hopefully) reconnect the second time.
- On a related note, essentially all WiFi APIs will fail if `Flash SPI speed` is set to `80 MHz` instead of `40 MHz` or below.
