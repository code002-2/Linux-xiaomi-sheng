# Sensor support

[中文](../传感器支持.md) | **English**

1. Check the sensor service status:

   ```bash
   sudo systemctl status iio-sensor-proxy
   sudo systemctl status adsprpcd-sensorspd
   ```

2. If they are not running, enable and start them:

   ```bash
   sudo systemctl enable iio-sensor-proxy
   sudo systemctl start iio-sensor-proxy
   sudo systemctl enable adsprpcd-sensorspd
   sudo systemctl start adsprpcd-sensorspd
   ```

3. Monitor the sensor data:

   ```bash
   monitor-sensor
   ```

   If the values change in real time, the sensors are working.
