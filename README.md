# xiaomigateway
The HomeAssiatant custom component. Uses python-miio package ( Vers.  >= 0.3.7 ) (https://github.com/rytilahti/python-miio/).
Allows you to manage the following devices connected to the XiaomiGateway:
- Lamp "Aqara LED Light Bulb (ZNLDP12LM)". Identifier in "MiHome": 'lumi.light.aqcn02'.
  Supports brightness and color temperature control.
- Two-channel relay "Aqara (LLRZMK11LM)". The identifier in "MiHome" is 'lumi.relay.c2acn01'.
  Support: Control channel_1 and channel_2, CURRENT_POWER, POWER_CONSUMED
- XiaomiGateway FM Radio.
  Support: Turn on/off, sound control (including MUTE), next station, previous station,
  flexible setting of stations, including favorites from "MiHome", select stations from the list.
  Simply add your various audio streams in M3U8 format, without using any tricks with MiHome


To enable "xiaomigateway" in your installation, the following instruction must be followed:
1. Copy directory "xiaomigateway" to you custom_component directory
2. Add to your configuration.yaml file:

== configuration.yaml ==

xiaomigateway:

    host: 192.168.0.1
    token: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    
    light:
      - sid: lumi.158d0003e99991
        name: LightName
        
    switch:
      - sid: lumi.158d0003c99991
        name: RelayName
        
    media_player:
        name: FmRadioName
        source_list: [
                Ретро FM,
                Детское радио,
                Дорожное радио,
                Радио Energy,
                Европа Плюс,
                Авторадио
            ]
        program_list: [
                [527782001],
                [527782002],
                [527782003],
                [527782004],
                [527782005],
                [1023,"http:\/\/192.168.0.254\/527782006.m3u8"]
            ]
            
== End configuration.yaml ==

CONFIGURATION VARIABLES


host
    (string) (Required)
    The host/IP address the of gateway.
    
token
    (string) (Required)
    The API token of your XiaomiGateway
    
light
    (map) (Required)
    A list of lights to set up.

    sid
        (string)(Required)
        The SID your Aqara LED Light Bulb.
    name
        (string)(Optional)
        The Name your Aqara LED Light Bulb
        
switch
    (map) (Required)
    A list of relays to set up.

    sid
        (string)(Required)
        The SID your Aqara Relay.
    name
        (string)(Optional)
        The Name your Aqara Relay.
        
media_player
    (map) (Required)
    Only element the XiaomiGateway FM Radio player.

    name
        (string)(Optional)
        The Name your FM Radio XiaomiGateway.
    source_list
        (list)(Required)
        Ordered list of Name your stantion.
        Each element of the list has type (string).
        List can be empty.
    program_list
        (list)(Required)
        List of broadcast source elements of radio stations. Each item in the list is of type (list).
        List cannot be empty
        The data format of each elment is list [ID, URL].
            ID
                (positive int)(Required)
                internal XiaomiGateway station ID, positive_int type.
                If this ID is from the list of favorite stations, the URL is not specified.
            URL
                (url)(Optional)
                link to the broadcast stream of the radio station in M3U8 format.
                Has the URL type.

(C) 2020 Igor A. Putintsev  ig.zero@rambler.ru
