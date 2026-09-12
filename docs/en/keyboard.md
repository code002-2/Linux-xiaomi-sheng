# Official keyboard support (Pogo Pin)

[中文](../官方键盘支持.md) | **English**

1. Check the service status:

   ```bash
   sudo systemctl status sheng-devauth
   ```

2. If it is not running, enable and start it:

   ```bash
   sudo systemctl enable sheng-devauth
   sudo systemctl start sheng-devauth
   ```

3. Reconnect the keyboard's Pogo Pin connector.
4. Check the service again — the line below means authentication succeeded:

   ```
   Sent pad token to kernel driver!
   ```

5. The Pogo Pin connector has to be reconnected after every reboot to complete keyboard authentication.
