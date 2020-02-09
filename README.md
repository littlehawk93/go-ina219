# INA-219 Sensor Go API

Provides an interface for using the INA-219 sensor on a Raspberry Pi via the I2C hardware interface.

You can Texas Instrument's official specifications for the INA-219 sensor [here](http://www.ti.com/lit/ds/symlink/ina219.pdf).

### Features

- Simple and easy interface for reading and configuring the INA-219 sensor
- Leverages [Periph.io](https://periph.io/)'s I2C library for low-level communication on Pi hardware
- Completely customizable behavior using the *ina219.Configuration* struct

### To-do

- More pre-built configurations for easier set up for common situations

### Installation

```
go get github.com/littlehawk93/go-ina219
```

### Getting Started

Simple reading values from the sensor

```

address := 64 // (Hex address 0x80 this is the default I2C address)

sensor, err := ina219.NewSensor(address, ina219.BusDefault)

if err != nil {
    log.Fatalf("Error initializing INA219 sensor: %s\n", err.Error())
}

defer sensor.Close()

// Get the current voltage being detected by the sensor (value in V)
voltage, _ := sensor.GetBusVoltage()

// Get the current being read by the sensor (value in mA)
current, _ := sensor.GetCurrent()

// Get the current power draw detected by the sensor (value in mW)
power, _ := sensor.GetPower()

```

Put sensor in power saving mode
```
if err := sensor.SetPowerSavingMode(true); err != nil {
    log.Fatalf("Unable to put INA-219 in power-saving mode: %s", err.Error())
}

time.Sleep(time.Second)

if err := sensor.SetPowerSavingMode(false); err != nil {
    log.Fatalf("Unable to wake INA-219 from power-saving mode: %s", err.Error())
}

```

More examples coming in the future!