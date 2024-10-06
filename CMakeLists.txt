# Check ESP-IDF version and error out if it is not in the supported range.
#
# Note for arduino-esp32 developers: to bypass the version check locally,
# set ARDUINO_SKIP_IDF_VERSION_CHECK environment variable to 1. For example:
#   export ARDUINO_SKIP_IDF_VERSION_CHECK=1
#   idf.py build

set(min_supported_idf_version "5.1.0")
set(max_supported_idf_version "5.1.99")
set(idf_version "${IDF_VERSION_MAJOR}.${IDF_VERSION_MINOR}.${IDF_VERSION_PATCH}")

if ("${idf_version}" AND NOT "$ENV{ARDUINO_SKIP_IDF_VERSION_CHECK}")
  if (idf_version VERSION_LESS min_supported_idf_version)
    message(FATAL_ERROR "Arduino-esp32 can be used with ESP-IDF versions "
                        "between ${min_supported_idf_version} and ${max_supported_idf_version}, "
                        "but an older version is detected: ${idf_version}.")
  endif()
  if (idf_version VERSION_GREATER max_supported_idf_version)
    message(FATAL_ERROR "Arduino-esp32 can be used with ESP-IDF versions "
                        "between ${min_supported_idf_version} and ${max_supported_idf_version}, "
                        "but a newer version is detected: ${idf_version}.")
  endif()
endif()

set(CORE_SRCS
  cores/esp32/base64.cpp
  cores/esp32/cbuf.cpp
  cores/esp32/chip-debug-report.cpp
  cores/esp32/esp32-hal-adc.c
  cores/esp32/esp32-hal-bt.c
  cores/esp32/esp32-hal-cpu.c
  cores/esp32/esp32-hal-dac.c
  cores/esp32/esp32-hal-gpio.c
  cores/esp32/esp32-hal-i2c.c
  cores/esp32/esp32-hal-i2c-slave.c
  cores/esp32/esp32-hal-ledc.c
  cores/esp32/esp32-hal-matrix.c
  cores/esp32/esp32-hal-misc.c
  cores/esp32/esp32-hal-periman.c
  cores/esp32/esp32-hal-psram.c
  cores/esp32/esp32-hal-rgb-led.c
  cores/esp32/esp32-hal-sigmadelta.c
  cores/esp32/esp32-hal-spi.c
  cores/esp32/esp32-hal-time.c
  cores/esp32/esp32-hal-timer.c
  cores/esp32/esp32-hal-tinyusb.c
  cores/esp32/esp32-hal-touch.c
  cores/esp32/esp32-hal-uart.c
  cores/esp32/esp32-hal-rmt.c
  cores/esp32/Esp.cpp
  cores/esp32/FunctionalInterrupt.cpp
  cores/esp32/HardwareSerial.cpp
  cores/esp32/HEXBuilder.cpp
  cores/esp32/IPAddress.cpp
  cores/esp32/libb64/cdecode.c
  cores/esp32/libb64/cencode.c
  cores/esp32/MacAddress.cpp
  cores/esp32/main.cpp
  cores/esp32/MD5Builder.cpp
  cores/esp32/Print.cpp
  cores/esp32/SHA1Builder.cpp
  cores/esp32/stdlib_noniso.c
  cores/esp32/Stream.cpp
  cores/esp32/StreamString.cpp
  cores/esp32/Tone.cpp
  cores/esp32/HWCDC.cpp
  cores/esp32/USB.cpp
  cores/esp32/USBCDC.cpp
  cores/esp32/USBMSC.cpp
  cores/esp32/FirmwareMSC.cpp
  cores/esp32/firmware_msc_fat.c
  cores/esp32/wiring_pulse.c
  cores/esp32/wiring_shift.c
  cores/esp32/WMath.cpp
  cores/esp32/WString.cpp
  )

set(ARDUINO_ALL_LIBRARIES
  ArduinoOTA
  AsyncUDP
  BLE
  BluetoothSerial
  DNSServer
  EEPROM
  ESP_I2S
  ESP_NOW
  ESP_SR
  ESPmDNS
  Ethernet
  FFat
  FS
  HTTPClient
  HTTPUpdate
  HX711
  Insights
  LittleFS
  NetBIOS
  Network
  NimBLE-Arduino
  OpenThread
  PPP
  Preferences
  RainMaker
  SD_MMC
  SD
  SimpleBLE
  SPIFFS
  SPI
  Ticker
  Update
  USB
  U8g2
  WebServer
  NetworkClientSecure
  WiFi
  WiFiProv
  Wire
  Zigbee
  )

set(ARDUINO_LIBRARY_ArduinoOTA_SRCS libraries/ArduinoOTA/src/ArduinoOTA.cpp)
set(ARDUINO_LIBRARY_ArduinoOTA_REQUIRES esp_https_ota)

set(ARDUINO_LIBRARY_AsyncUDP_SRCS libraries/AsyncUDP/src/AsyncUDP.cpp)

set(ARDUINO_LIBRARY_BluetoothSerial_SRCS
  libraries/BluetoothSerial/src/BluetoothSerial.cpp
  libraries/BluetoothSerial/src/BTAddress.cpp
  libraries/BluetoothSerial/src/BTAdvertisedDeviceSet.cpp
  libraries/BluetoothSerial/src/BTScanResultsSet.cpp)

set(ARDUINO_LIBRARY_DNSServer_SRCS libraries/DNSServer/src/DNSServer.cpp)

set(ARDUINO_LIBRARY_EEPROM_SRCS libraries/EEPROM/src/EEPROM.cpp)

set(ARDUINO_LIBRARY_ESP_I2S_SRCS libraries/ESP_I2S/src/ESP_I2S.cpp)

set(ARDUINO_LIBRARY_ESP_NOW_SRCS
  libraries/ESP_NOW/src/ESP32_NOW.cpp
  libraries/ESP_NOW/src/ESP32_NOW_Serial.cpp)

set(ARDUINO_LIBRARY_ESP_SR_SRCS
  libraries/ESP_SR/src/ESP_SR.cpp
  libraries/ESP_SR/src/esp32-hal-sr.c)

set(ARDUINO_LIBRARY_ESPmDNS_SRCS libraries/ESPmDNS/src/ESPmDNS.cpp)

set(ARDUINO_LIBRARY_Ethernet_SRCS libraries/Ethernet/src/ETH.cpp)

set(ARDUINO_LIBRARY_FFat_SRCS libraries/FFat/src/FFat.cpp)

set(ARDUINO_LIBRARY_FS_SRCS
  libraries/FS/src/FS.cpp
  libraries/FS/src/vfs_api.cpp)

set(ARDUINO_LIBRARY_HTTPClient_SRCS libraries/HTTPClient/src/HTTPClient.cpp)

set(ARDUINO_LIBRARY_HTTPUpdate_SRCS libraries/HTTPUpdate/src/HTTPUpdate.cpp)

set(ARDUINO_LIBRARY_HX711_SRCS libraries/HX711/src/HX711.cpp)

set(ARDUINO_LIBRARY_Insights_SRCS libraries/Insights/src/Insights.cpp)

set(ARDUINO_LIBRARY_LittleFS_SRCS libraries/LittleFS/src/LittleFS.cpp)

set(ARDUINO_LIBRARY_NetBIOS_SRCS libraries/NetBIOS/src/NetBIOS.cpp)

set(ARDUINO_LIBRARY_NimBLE-Arduino_SRCS
  libraries/NimBLE-Arduino/src/NimBLEAdvertisedDevice.cpp
  libraries/NimBLE-Arduino/src/NimBLEDescriptor.cpp
  libraries/NimBLE-Arduino/src/NimBLEClient.cpp
  libraries/NimBLE-Arduino/src/NimBLEAdvertising.cpp
  libraries/NimBLE-Arduino/src/NimBLEAddress.cpp
  libraries/NimBLE-Arduino/src/NimBLEUUID.cpp
  libraries/NimBLE-Arduino/src/NimBLEService.cpp
  libraries/NimBLE-Arduino/src/NimBLERemoteDescriptor.cpp
  libraries/NimBLE-Arduino/src/NimBLEDevice.cpp
  libraries/NimBLE-Arduino/src/NimBLEExtAdvertising.cpp
  libraries/NimBLE-Arduino/src/NimBLERemoteCharacteristic.cpp
  libraries/NimBLE-Arduino/src/NimBLERemoteService.cpp
  libraries/NimBLE-Arduino/src/NimBLECharacteristic.cpp
  libraries/NimBLE-Arduino/src/NimBLESecurity.cpp
  libraries/NimBLE-Arduino/src/NimBLE2904.cpp
  libraries/NimBLE-Arduino/src/NimBLEScan.cpp
  libraries/NimBLE-Arduino/src/NimBLEBeacon.cpp
  libraries/NimBLE-Arduino/src/NimBLEUtils.cpp
  libraries/NimBLE-Arduino/src/nimble/esp_port/esp-hci/src/esp_nimble_hci.c
  libraries/NimBLE-Arduino/src/nimble/esp_port/port/src/esp_nimble_mem.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/hmac.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/ctr_mode.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/ecc_dsa.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/ecc_platform_specific.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/ecc.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/cmac_mode.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/aes_decrypt.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/ctr_prng.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/utils.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/aes_encrypt.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/cbc_mode.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/ccm_mode.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/sha256.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/ecc_dh.c
  libraries/NimBLE-Arduino/src/nimble/ext/tinycrypt/src/hmac_prng.c
  libraries/NimBLE-Arduino/src/nimble/nimble/drivers/nrf51/src/ble_hw.c
  libraries/NimBLE-Arduino/src/nimble/nimble/drivers/nrf51/src/ble_phy.c
  libraries/NimBLE-Arduino/src/nimble/nimble/drivers/nrf52/src/ble_hw.c
  libraries/NimBLE-Arduino/src/nimble/nimble/drivers/nrf52/src/ble_phy_trace.c
  libraries/NimBLE-Arduino/src/nimble/nimble/drivers/nrf52/src/ble_phy.c
  libraries/NimBLE-Arduino/src/nimble/nimble/transport/ram/src/ble_hci_ram.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/proxy.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/health_cli.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/nodes.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/transport.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/subnet.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/model_cli.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/aes-ccm.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/prov_device.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/access.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/cfg.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/light_model.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/cdb.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/pb_adv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/cfg_cli.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/shell.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/health_srv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/model_srv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/settings.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/beacon.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/net.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/lpn.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/friend.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/app_keys.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/prov.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/provisioner.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/pb_gatt.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/heartbeat.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/crypto.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/mesh.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/adv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/cfg_srv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/glue.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/mesh/src/rpl.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/util/src/addr.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/ias/src/ble_svc_ias.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/ans/src/ble_svc_ans.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/gatt/src/ble_svc_gatt.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/ipss/src/ble_svc_ipss.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/gap/src/ble_svc_gap.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/lls/src/ble_svc_lls.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/dis/src/ble_svc_dis.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/services/bas/src/ble_svc_bas.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/store/config/src/ble_store_nvs.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/store/config/src/ble_store_config_conf.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/store/config/src/ble_store_config.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_store_util.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_startup.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_att_cmd.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_conn.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_l2cap.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_log.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_resolv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_mbuf.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_id.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_mqueue.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_periodic_sync.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_store.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_sm.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_cfg.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_l2cap_sig.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_gattc.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_flow.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_gap.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_eddystone.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_hci.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_att_clt.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_hci_cmd.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_ibeacon.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_misc.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_sm_cmd.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_l2cap_coc.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_shutdown.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_atomic.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_sm_sc.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_sm_lgcy.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_adv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_uuid.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_gatts_lcl.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_stop.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_l2cap_sig_cmd.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_hci_util.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_gatts.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_hci_evt.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_hs_pvcy.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_att_svr.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_monitor.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_sm_alg.c
  libraries/NimBLE-Arduino/src/nimble/nimble/host/src/ble_att.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_sched.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_conn.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_scan.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_trace.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_supp_cmd.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_dtm.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_rand.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_ctrl.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_adv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_rfmgmt.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_utils.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_resolv.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_iso.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_hci.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_conn_hci.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_sync.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_hci_ev.c
  libraries/NimBLE-Arduino/src/nimble/nimble/controller/src/ble_ll_whitelist.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/hal_timer.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/os_mbuf.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/nimble_port.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/mem.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/os_cputime_pwr2.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/hal_uart.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/os_mempool.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/os_cputime.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/endian.c
  libraries/NimBLE-Arduino/src/nimble/porting/nimble/src/os_msys_init.c
  libraries/NimBLE-Arduino/src/nimble/porting/npl/freertos/src/nimble_port_freertos.c
  libraries/NimBLE-Arduino/src/nimble/porting/npl/freertos/src/npl_os_freertos.c
  libraries/NimBLE-Arduino/src/NimBLEEddystoneURL.cpp
  libraries/NimBLE-Arduino/src/NimBLEHIDDevice.cpp
  libraries/NimBLE-Arduino/src/NimBLEServer.cpp
  libraries/NimBLE-Arduino/src/NimBLEEddystoneTLM.cpp)

set(ARDUINO_LIBRARY_OpenThread_SRCS
  libraries/OpenThread/src/OThreadCLI.cpp
  libraries/OpenThread/src/OThreadCLI_Util.cpp)

set(ARDUINO_LIBRARY_PPP_SRCS
  libraries/PPP/src/PPP.cpp
  libraries/PPP/src/ppp.c)

set(ARDUINO_LIBRARY_Preferences_SRCS libraries/Preferences/src/Preferences.cpp)

set(ARDUINO_LIBRARY_RainMaker_SRCS
  libraries/RainMaker/src/RMaker.cpp
  libraries/RainMaker/src/RMakerNode.cpp
  libraries/RainMaker/src/RMakerParam.cpp
  libraries/RainMaker/src/RMakerDevice.cpp
  libraries/RainMaker/src/RMakerType.cpp
  libraries/RainMaker/src/RMakerQR.cpp
  libraries/RainMaker/src/RMakerUtils.cpp
  libraries/RainMaker/src/AppInsights.cpp)

set(ARDUINO_LIBRARY_SD_MMC_SRCS libraries/SD_MMC/src/SD_MMC.cpp)

set(ARDUINO_LIBRARY_SD_SRCS
  libraries/SD/src/SD.cpp
  libraries/SD/src/sd_diskio.cpp
  libraries/SD/src/sd_diskio_crc.c)

set(ARDUINO_LIBRARY_SimpleBLE_SRCS libraries/SimpleBLE/src/SimpleBLE.cpp)

set(ARDUINO_LIBRARY_SPIFFS_SRCS libraries/SPIFFS/src/SPIFFS.cpp)

set(ARDUINO_LIBRARY_SPI_SRCS libraries/SPI/src/SPI.cpp)

set(ARDUINO_LIBRARY_Ticker_SRCS libraries/Ticker/src/Ticker.cpp)

set(ARDUINO_LIBRARY_Update_SRCS
  libraries/Update/src/Updater.cpp
  libraries/Update/src/HttpsOTAUpdate.cpp)

set(ARDUINO_LIBRARY_USB_SRCS
  libraries/USB/src/USBHID.cpp
  libraries/USB/src/USBMIDI.cpp
  libraries/USB/src/USBHIDMouse.cpp
  libraries/USB/src/USBHIDKeyboard.cpp
  libraries/USB/src/USBHIDGamepad.cpp
  libraries/USB/src/USBHIDConsumerControl.cpp
  libraries/USB/src/USBHIDSystemControl.cpp
  libraries/USB/src/USBHIDVendor.cpp
  libraries/USB/src/USBVendor.cpp)

set(ARDUINO_LIBRARY_U8g2_SRCS
  libraries/U8g2/src/U8x8lib.cpp
  libraries/U8g2/src/U8g2lib.cpp
  libraries/U8g2/src/clib/u8x8_cad.c
  libraries/U8g2/src/clib/u8x8_d_lc7981.c
  libraries/U8g2/src/clib/u8x8_d_st7567.c
  libraries/U8g2/src/clib/u8x8_d_sh1108.c
  libraries/U8g2/src/clib/u8g2_fonts.c
  libraries/U8g2/src/clib/u8x8_d_ssd1317.c
  libraries/U8g2/src/clib/u8x8_d_ist7920.c
  libraries/U8g2/src/clib/u8g2_kerning.c
  libraries/U8g2/src/clib/u8x8_d_uc1617.c
  libraries/U8g2/src/clib/u8x8_d_uc1701_dogs102.c
  libraries/U8g2/src/clib/u8g2_d_setup.c
  libraries/U8g2/src/clib/u8x8_d_st75160.c
  libraries/U8g2/src/clib/u8x8_d_st75320.c
  libraries/U8g2/src/clib/u8x8_d_max7219.c
  libraries/U8g2/src/clib/u8x8_d_uc1638.c
  libraries/U8g2/src/clib/u8x8_d_ssd1362.c
  libraries/U8g2/src/clib/u8x8_d_ssd1309.c
  libraries/U8g2/src/clib/u8g2_arc.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_96x16.c
  libraries/U8g2/src/clib/u8x8_d_st7586s_ymc240160.c
  libraries/U8g2/src/clib/u8x8_d_pcd8544_84x48.c
  libraries/U8g2/src/clib/u8g2_input_value.c
  libraries/U8g2/src/clib/u8g2_cleardisplay.c
  libraries/U8g2/src/clib/u8g2_ll_hvline.c
  libraries/U8g2/src/clib/u8g2_setup.c
  libraries/U8g2/src/clib/u8x8_d_uc1628.c
  libraries/U8g2/src/clib/u8x8_capture.c
  libraries/U8g2/src/clib/u8x8_d_ssd1607_200x200.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_48x64.c
  libraries/U8g2/src/clib/u8x8_d_ssd1326.c
  libraries/U8g2/src/clib/u8x8_d_ssd1322.c
  libraries/U8g2/src/clib/u8x8_debounce.c
  libraries/U8g2/src/clib/u8x8_d_ks0108.c
  libraries/U8g2/src/clib/u8x8_d_st7586s_jlx320160.c
  libraries/U8g2/src/clib/u8x8_d_ch1120.c
  libraries/U8g2/src/clib/u8x8_d_uc1609.c
  libraries/U8g2/src/clib/u8x8_d_st7302.c
  libraries/U8g2/src/clib/u8log.c
  libraries/U8g2/src/clib/u8x8_d_st7539.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_2040x16.c
  libraries/U8g2/src/clib/u8x8_d_uc1610.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_128x32.c
  libraries/U8g2/src/clib/u8x8_message.c
  libraries/U8g2/src/clib/u8x8_d_ssd1606_172x72.c
  libraries/U8g2/src/clib/u8x8_d_s1d15300.c
  libraries/U8g2/src/clib/u8x8_d_ist3020.c
  libraries/U8g2/src/clib/u8x8_setup.c
  libraries/U8g2/src/clib/u8x8_d_il3820_296x128.c
  libraries/U8g2/src/clib/u8x8_d_ssd1325.c
  libraries/U8g2/src/clib/u8x8_d_st7511.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_64x48.c
  libraries/U8g2/src/clib/u8x8_d_uc1604.c
  libraries/U8g2/src/clib/u8x8_8x8.c
  libraries/U8g2/src/clib/u8log_u8g2.c
  libraries/U8g2/src/clib/u8x8_d_st7586s_jlx384160.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_128x64_noname.c
  libraries/U8g2/src/clib/u8x8_fonts.c
  libraries/U8g2/src/clib/u8x8_d_st75256.c
  libraries/U8g2/src/clib/u8x8_d_st7301.c
  libraries/U8g2/src/clib/u8x8_d_s1d15721.c
  libraries/U8g2/src/clib/u8g2_circle.c
  libraries/U8g2/src/clib/u8x8_d_sbn1661.c
  libraries/U8g2/src/clib/u8g2_box.c
  libraries/U8g2/src/clib/u8x8_d_uc1611.c
  libraries/U8g2/src/clib/u8x8_d_gp1287ai.c
  libraries/U8g2/src/clib/u8g2_intersection.c
  libraries/U8g2/src/clib/u8log_u8x8.c
  libraries/U8g2/src/clib/u8x8_d_st7565.c
  libraries/U8g2/src/clib/u8x8_d_st7588.c
  libraries/U8g2/src/clib/u8x8_d_sh1106_64x32.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_64x32.c
  libraries/U8g2/src/clib/u8g2_message.c
  libraries/U8g2/src/clib/u8x8_d_gp1247ai.c
  libraries/U8g2/src/clib/u8x8_d_pcf8812.c
  libraries/U8g2/src/clib/u8g2_bitmap.c
  libraries/U8g2/src/clib/u8x8_d_uc1701_mini12864.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_96x40.c
  libraries/U8g2/src/clib/u8x8_d_t6963.c
  libraries/U8g2/src/clib/u8x8_u8toa.c
  libraries/U8g2/src/clib/u8x8_d_ist3088.c
  libraries/U8g2/src/clib/u8x8_d_st7586s_md240128.c
  libraries/U8g2/src/clib/u8x8_d_st7586s_erc240160.c
  libraries/U8g2/src/clib/u8x8_d_st7571.c
  libraries/U8g2/src/clib/u8x8_display.c
  libraries/U8g2/src/clib/u8x8_d_gp1294ai.c
  libraries/U8g2/src/clib/u8x8_gpio.c
  libraries/U8g2/src/clib/u8x8_d_uc1601.c
  libraries/U8g2/src/clib/u8x8_d_sed1330.c
  libraries/U8g2/src/clib/u8x8_d_st7920.c
  libraries/U8g2/src/clib/u8x8_d_ssd1305.c
  libraries/U8g2/src/clib/u8x8_d_ssd1320.c
  libraries/U8g2/src/clib/u8g2_selection_list.c
  libraries/U8g2/src/clib/u8x8_d_s1d15e06.c
  libraries/U8g2/src/clib/u8x8_d_hd44102.c
  libraries/U8g2/src/clib/u8x8_d_ld7032_60x32.c
  libraries/U8g2/src/clib/u8g2_buffer.c
  libraries/U8g2/src/clib/u8x8_selection_list.c
  libraries/U8g2/src/clib/u8x8_d_st7528.c
  libraries/U8g2/src/clib/mui.c
  libraries/U8g2/src/clib/u8x8_d_ssd1316.c
  libraries/U8g2/src/clib/u8g2_line.c
  libraries/U8g2/src/clib/u8g2_font.c
  libraries/U8g2/src/clib/u8x8_d_st75161.c
  libraries/U8g2/src/clib/u8x8_d_ssd1312.c
  libraries/U8g2/src/clib/u8x8_d_sh1122.c
  libraries/U8g2/src/clib/u8g2_d_memory.c
  libraries/U8g2/src/clib/u8x8_d_ssd1318.c
  libraries/U8g2/src/clib/u8x8_string.c
  libraries/U8g2/src/clib/u8x8_d_st7586s_s028hn118a.c
  libraries/U8g2/src/clib/u8x8_d_sh1107.c
  libraries/U8g2/src/clib/u8g2_button.c
  libraries/U8g2/src/clib/u8x8_d_pcf8814_hx1230.c
  libraries/U8g2/src/clib/u8g2_polygon.c
  libraries/U8g2/src/clib/u8x8_u16toa.c
  libraries/U8g2/src/clib/u8x8_input_value.c
  libraries/U8g2/src/clib/u8x8_d_ssd1363.c
  libraries/U8g2/src/clib/mui_u8g2.c
  libraries/U8g2/src/clib/u8x8_d_a2printer.c
  libraries/U8g2/src/clib/u8x8_byte.c
  libraries/U8g2/src/clib/u8x8_d_ssd1327.c
  libraries/U8g2/src/clib/u8x8_d_ssd1306_72x40.c
  libraries/U8g2/src/clib/u8x8_d_ssd1329.c
  libraries/U8g2/src/clib/u8x8_d_ls013b7dh03.c
  libraries/U8g2/src/clib/u8x8_d_sh1106_72x40.c
  libraries/U8g2/src/clib/u8g2_hvline.c
  libraries/U8g2/src/clib/u8x8_d_gu800.c
  libraries/U8g2/src/clib/u8x8_d_uc1608.c)

set(ARDUINO_LIBRARY_WebServer_SRCS
  libraries/WebServer/src/WebServer.cpp
  libraries/WebServer/src/Parsing.cpp
  libraries/WebServer/src/detail/mimetable.cpp)

set(ARDUINO_LIBRARY_NetworkClientSecure_SRCS
  libraries/NetworkClientSecure/src/ssl_client.cpp
  libraries/NetworkClientSecure/src/NetworkClientSecure.cpp)

set(ARDUINO_LIBRARY_Network_SRCS
  libraries/Network/src/NetworkInterface.cpp
  libraries/Network/src/NetworkEvents.cpp
  libraries/Network/src/NetworkManager.cpp
  libraries/Network/src/NetworkClient.cpp
  libraries/Network/src/NetworkServer.cpp
  libraries/Network/src/NetworkUdp.cpp)

set(ARDUINO_LIBRARY_WiFi_SRCS
  libraries/WiFi/src/WiFiAP.cpp
  libraries/WiFi/src/WiFi.cpp
  libraries/WiFi/src/WiFiGeneric.cpp
  libraries/WiFi/src/WiFiMulti.cpp
  libraries/WiFi/src/WiFiScan.cpp
  libraries/WiFi/src/WiFiSTA.cpp
  libraries/WiFi/src/STA.cpp
  libraries/WiFi/src/AP.cpp)

set(ARDUINO_LIBRARY_WiFiProv_SRCS libraries/WiFiProv/src/WiFiProv.cpp)

set(ARDUINO_LIBRARY_Wire_SRCS libraries/Wire/src/Wire.cpp)

set(ARDUINO_LIBRARY_Zigbee_SRCS
  libraries/Zigbee/src/ZigbeeCore.cpp
  libraries/Zigbee/src/ZigbeeEP.cpp
  libraries/Zigbee/src/ZigbeeHandlers.cpp
  libraries/Zigbee/src/ep/ZigbeeColorDimmableLight.cpp
  libraries/Zigbee/src/ep/ZigbeeColorDimmerSwitch.cpp
  libraries/Zigbee/src/ep/ZigbeeLight.cpp
  libraries/Zigbee/src/ep/ZigbeeSwitch.cpp
  libraries/Zigbee/src/ep/ZigbeeTempSensor.cpp
  libraries/Zigbee/src/ep/ZigbeeThermostat.cpp
  )

set(ARDUINO_LIBRARY_BLE_SRCS
  libraries/BLE/src/BLE2901.cpp
  libraries/BLE/src/BLE2902.cpp
  libraries/BLE/src/BLE2904.cpp
  libraries/BLE/src/BLEAddress.cpp
  libraries/BLE/src/BLEAdvertisedDevice.cpp
  libraries/BLE/src/BLEAdvertising.cpp
  libraries/BLE/src/BLEBeacon.cpp
  libraries/BLE/src/BLECharacteristic.cpp
  libraries/BLE/src/BLECharacteristicMap.cpp
  libraries/BLE/src/BLEClient.cpp
  libraries/BLE/src/BLEDescriptor.cpp
  libraries/BLE/src/BLEDescriptorMap.cpp
  libraries/BLE/src/BLEDevice.cpp
  libraries/BLE/src/BLEEddystoneTLM.cpp
  libraries/BLE/src/BLEEddystoneURL.cpp
  libraries/BLE/src/BLEExceptions.cpp
  libraries/BLE/src/BLEHIDDevice.cpp
  libraries/BLE/src/BLERemoteCharacteristic.cpp
  libraries/BLE/src/BLERemoteDescriptor.cpp
  libraries/BLE/src/BLERemoteService.cpp
  libraries/BLE/src/BLEScan.cpp
  libraries/BLE/src/BLESecurity.cpp
  libraries/BLE/src/BLEServer.cpp
  libraries/BLE/src/BLEService.cpp
  libraries/BLE/src/BLEServiceMap.cpp
  libraries/BLE/src/BLEUtils.cpp
  libraries/BLE/src/BLEUUID.cpp
  libraries/BLE/src/BLEValue.cpp
  libraries/BLE/src/FreeRTOS.cpp
  libraries/BLE/src/GeneralUtils.cpp
  )

set(ARDUINO_LIBRARIES_SRCS)
set(ARDUINO_LIBRARIES_REQUIRES)
set(ARDUINO_LIBRARIES_INCLUDEDIRS)
foreach(libname IN LISTS ARDUINO_ALL_LIBRARIES)
  if(NOT CONFIG_ARDUINO_SELECTIVE_COMPILATION OR CONFIG_ARDUINO_SELECTIVE_${libname})
    if(ARDUINO_LIBRARY_${libname}_SRCS)
      list(APPEND ARDUINO_LIBRARIES_SRCS ${ARDUINO_LIBRARY_${libname}_SRCS})
    endif()
    if(ARDUINO_LIBRARY_${libname}_REQUIRES)
      list(APPEND ARDUINO_LIBRARIES_REQUIRES ${ARDUINO_LIBRARY_${libname}_REQUIRES})
    endif()
    if(EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/libraries/${libname}/src)
      list(APPEND ARDUINO_LIBRARIES_INCLUDEDIRS libraries/${libname}/src)
    endif()
  endif()
endforeach()

set(includedirs variants/${CONFIG_ARDUINO_VARIANT}/ cores/esp32/ ${ARDUINO_LIBRARIES_INCLUDEDIRS})
set(srcs ${CORE_SRCS} ${ARDUINO_LIBRARIES_SRCS})
set(priv_includes cores/esp32/libb64)
set(requires spi_flash esp_partition mbedtls wpa_supplicant esp_adc esp_eth http_parser espressif__network_provisioning)
set(priv_requires fatfs nvs_flash app_update spiffs bootloader_support bt esp_hid usb esp_psram ${ARDUINO_LIBRARIES_REQUIRES})

if(NOT CONFIG_ARDUINO_SELECTIVE_COMPILATION OR CONFIG_ARDUINO_SELECTIVE_OpenThread)
  #if(CONFIG_SOC_IEEE802154_SUPPORTED) # Does not work!
  #if(CONFIG_OPENTHREAD_ENABLED) # Does not work!
  if(IDF_TARGET STREQUAL "esp32c6" OR IDF_TARGET STREQUAL "esp32h2") # Sadly only this works
    list(APPEND requires openthread)
  endif()
endif()

idf_component_register(INCLUDE_DIRS ${includedirs} PRIV_INCLUDE_DIRS ${priv_includes} SRCS ${srcs} REQUIRES ${requires} PRIV_REQUIRES ${priv_requires})

if(NOT CONFIG_FREERTOS_HZ EQUAL 1000 AND NOT "$ENV{ARDUINO_SKIP_TICK_CHECK}")
    # See delay() in cores/esp32/esp32-hal-misc.c.
    message(FATAL_ERROR "esp32-arduino requires CONFIG_FREERTOS_HZ=1000 "
                        "(currently ${CONFIG_FREERTOS_HZ})")
endif()

string(TOUPPER ${CONFIG_ARDUINO_VARIANT} idf_target_caps)
string(REPLACE "-" "_" idf_target_for_macro "${idf_target_caps}")
target_compile_options(${COMPONENT_TARGET} PUBLIC
    -DARDUINO=10812
    -DARDUINO_${idf_target_for_macro}_DEV
    -DARDUINO_ARCH_ESP32
    -DARDUINO_BOARD="${idf_target_caps}_DEV"
    -DARDUINO_VARIANT="${CONFIG_ARDUINO_VARIANT}"
    -DESP32=ESP32)

if(CONFIG_AUTOSTART_ARDUINO)
    # in autostart mode, arduino-esp32 contains app_main() function and needs to
    # reference setup() and loop() in the main component. If we add main
    # component to priv_requires then we create a large circular dependency
    # (arduino-esp32 -> main -> arduino-esp32) and can get linker errors, so
    # instead we add setup() and loop() to the undefined symbols list so the
    # linker will always include them.
    #
    # (As they are C++ symbol, we need to add the C++ mangled names.)
    target_link_libraries(${COMPONENT_LIB} INTERFACE "-u _Z5setupv -u _Z4loopv")
endif()

# This function adds a dependency on the given component if the component is included into the build.
function(maybe_add_component component_name)
    idf_build_get_property(components BUILD_COMPONENTS)
    if (${component_name} IN_LIST components)
        idf_component_get_property(lib_name ${component_name} COMPONENT_LIB)
        target_link_libraries(${COMPONENT_LIB} PUBLIC ${lib_name})
    endif()
endfunction()

if(IDF_TARGET MATCHES "esp32s2|esp32s3" AND CONFIG_TINYUSB_ENABLED)
    maybe_add_component(arduino_tinyusb)
endif()
if(NOT CONFIG_ARDUINO_SELECTIVE_COMPILATION OR CONFIG_ARDUINO_SELECTIVE_ArduinoOTA)
    maybe_add_component(esp_https_ota)
endif()
