# Samsung_S8_FRP_Hacking
    Bypass Factory Reset Protection on any Samsung Galaxy S8 model on Android 7.0 Nougat or later.

### Install heimdall
    echo -e "# Heimdall (Flashtool for Sasmung Devices)\napp-mobilephone/heimdall qt5" >> /etc/portage/package.use/use
    emerge --ask app-mobilephone/heimdall

### Detect Device:
    heimdall detect

### Download PIT:
    heimdall download-pit --no-reboot --output mydevice.pit

### Print PIT:
    heimdall print-pit --no-reboot --file mydevice.pit

### Boot device into flash mode:
    Poweroff device
    Press vol dn+powerbutton

### Flash your device with the customized rom 
###### Go found a rom on the net

### AFter flash has been done, device will reboot, here is some pics how it should look a like: 

# Once booted into FACTORY BINARY, see picture below, here is some hidden tips and tricks from myself ;-)



### Open notification bar: 

#### Its not possible to expand notification bar without touchscreen but with this trick it gonna work and you will have access to all settings by press in upper right corner on the setting icon;)
#### List settings
adb shell content query --uri content://settings/secure
adb shell content insert --uri content://settings/secure --bind name:s:user_setup_complete --bind value:s:1
#### Verify the value
adb shell content query --uri content://settings/secure|grep name=user_setup_complete|awk -F'value=' '{print $2}'|cut -d, -f1
##### Turn off location
adb shell content insert --uri content://settings/secure --bind name:s:location_previous_mode --bind value:s:0
adb shell content insert --uri content://settings/secure --bind name:s:location_providers_allowed --bind value:s:0
##### Turn on accessibility 
adb shell content insert --uri content://settings/secure --bind name:s:accessibility_enabled  --bind value:s:1
##### Turn on accessibility injection
adb shell content insert --uri content://settings/secure --bind name:s:accessibility_script_injection,  --bind value:s:1
##### Allow non market apps
adb shell content insert --uri content://settings/secure --bind name:s:install_non_market_apps  --bind value:s:1
##### Allow push notifications and also recive sms with a popup in notifications for example:
adb shell content insert --uri content://settings/secure --bind name:s:show_note_about_notification_hiding  --bind value:s:1
##### Disable lock feature:
adb shell content insert --uri content://settings/secure --bind name:s:lock_function_val  --bind value:s:0

#####
adb shell cmd statusbar expand-notifications 
or
am mCurrentFocus=Window{51e697dd0 u0 com.android.settings/com.android.settings.Settings}
