# Makerspace Checkin

This is a GUI Python program which records a maker (user) check-in
and check-out to a makerspace via an ID card tap. It is designed
to be run on a Raspberry Pi with a USB HID OmniKey card reader
connected. The card readers are configured by the MIT security
team to read the prox chip on MIT ID cards or the MIT Digital ID
off an Android or iOS device.


## Raspberry Pi Setup

### Power-off and Reboots

With the Raspberry Pi basically running as an always-on kiosk,
it is difficult to avoid the occasional power-cycle or loss
of line power.

If using a Raspberry Pi 3, it is recommended to run the Pi with
the overlay file system enabled. This leaves the microSD card
in read-only mode. It makes changes and updates a little more
onerous, requiring disabling the overlay file system, rebooting
into read-write mode, making changes, and then re-enabling the
overlay file system. However, it makes it safe to power-cycle
the Raspberry Pi.

If using a Raspberry Pi 4 or later, it can also be run with
the overlay file system enabled. In addition, it is recommended
to wire the Pi with a safe shutdown button. This can be done
by connecting a momentary normally-open push-button between GPIO 3 and GND.
Edit `/boot/config.txt` and add the line `dtoverlay=gpio-shutdown`.
The configuration line can be modified by appending `,gpio_pin=##` 
or `,active_low=0` or both to specify a GPIO pin other than the
default, and to use a normally-closed switch, respectively.

Pressing the button should now initiate a safe shutdown and
halt the Pi, with a short blinking of its activity LED to confirm
shutdown. Pressing the button again will start the Pi up from
its halted state.

## Makerspace Checkin Program Setup

### Requirements

The standard Raspberry Pi OS installation will contain most needed Python
modules. Ones that are not installed by default are listed in `requirements.txt`.
To install them use:

```
pip install -r requirements.txt
```

or

```
pip install -r requirements.txt --break-system-packages
```

if necessary.

### Environment

The application will need a `secrets.py` configuration file in its root directory.
This file contains configuration information for the specific makerspace, as well
as API keys for Airtable API and for MIT APIs.

```
#
# Credentials for Project Manus system
#
secrets = {
        'airtable_pat' : '<AIRTABLE PERSONAL ACCESS TOKEN>',
        'people_client_id' : '<MIT PEOPLE API CLIENT ID>',
        'people_client_secret' : '<MIT PEOPLE API CLIENT SECRET>,'
        'card_client_id' : '<MIT CARD API CLIENT ID>',
        'card_client_secret' : '<MIT CARD API CLIENT SECRET>'
}

#
# Shop Information
#
site = {
        'title' : '<SHOP TITLE TO DISPLAY IN APP>',
        'name' : '<SHOP NAME FROM AIRTABLE>',
        'description' : '<SHORT SHOP DESCRIPTION>',
        # Highlight colors for kiosk app
        'color-1' : '#57B99D',
        'color-2' : '#3D816E'
}

#
# A survey question.  Example is used in Project Manus makerspaces.
#
question = {
        'question' : 'What brings you to {} today?'.format(site['title']),
        'answers' : ['PERSONAL','RESEARCH','TRAINING','ENTREPRENEURSHIP','ON DUTY','CLUBS AND TEAMS','OTHER'],
        # leave 'freeform' blank to skip asking this question
        'freeform' : 'or enter class number'
}

#
# Full path to log file.  Null logs to stdio
#
logs = {
        'logfile' : ''
}

```
