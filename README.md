# DHT22 / AM2302 C/C++ library for ESP32 (ESP-IDF)

This is an ESP32 C/C++ (esp-idf) library for the DHT22 low cost temperature/humidity sensors.

C version Based on: https://github.com/gosouth/DHT22

C++ version Based on: https://github.com/gosouth/DHT22-cpp


**USE IN C**

See examples/Example on C/main.c

```C
void DHT_task(void *pvParameter)
{
    setDHTgpio(GPIO_NUM_4);
    ESP_LOGI(TAG, "Starting DHT Task\n\n");

    while (1)
    {
        ESP_LOGI(TAG, "=== Reading DHT ===\n");
        int ret = readDHT();

        errorHandler(ret);

        ESP_LOGI(TAG, "Hum: %.1f Tmp: %.1f\n", getHumidity(), getTemperature());

        // -- wait at least 3 sec before reading again ------------
        // The interval of whole process must be beyond 2 seconds !!
        vTaskDelay(3000 / portTICK_PERIOD_MS);
    }
}

void app_main()
{
    // Initialize NVS
    esp_err_t ret = nvs_flash_init();
    if (ret == ESP_ERR_NVS_NO_FREE_PAGES)
    {
        ESP_ERROR_CHECK(nvs_flash_erase());
        ret = nvs_flash_init();
    }
    ESP_ERROR_CHECK(ret);

    esp_log_level_set("*", ESP_LOG_INFO);

    esp_rom_gpio_pad_select_gpio(GPIO_NUM_4);

    xTaskCreate(&DHT_task, "DHT_task", 2048, NULL, 5, NULL);
}
```
**USE IN C++**

See examples/Example on C++/main.cpp

```C
void DHT_task(void *pvParameter)
{
    DHT dht;
    dht.setDHTgpio(GPIO_NUM_4);
    ESP_LOGI(TAG, "Starting DHT Task\n\n");

    while (1)
    {
        ESP_LOGI(TAG, "=== Reading DHT ===\n");
        int ret = dht.readDHT();

        dht.errorHandler(ret);

        ESP_LOGI(TAG, "Hum: %.1f Tmp: %.1f\n", dht.getHumidity(), dht.getTemperature());

        // -- wait at least 3 sec before reading again ------------
        // The interval of whole process must be beyond 2 seconds !!
        vTaskDelay(3000 / portTICK_PERIOD_MS);
    }
}

void app_main()
{
    // Initialize NVS
    esp_err_t ret = nvs_flash_init();
    if (ret == ESP_ERR_NVS_NO_FREE_PAGES)
    {
        ESP_ERROR_CHECK(nvs_flash_erase());
        ret = nvs_flash_init();
    }
    ESP_ERROR_CHECK(ret);

    esp_log_level_set("*", ESP_LOG_INFO);

    esp_rom_gpio_pad_select_gpio(GPIO_NUM_4);

    xTaskCreate(&DHT_task, "DHT_task", 2048, NULL, 5, NULL);
}
```

Copyright (c) 2022 ANDREY MITROKHIN.

All rights reserved.