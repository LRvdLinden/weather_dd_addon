<h1 align="center">Weather Dashboard - Dwains Dashboard Add-on (more_page)</h1> 


<p align="center">
  <a href="https://dwainscheeren.github.io/dwains-lovelace-dashboard/">
    <img src="https://img.shields.io/badge/Dwains%20Dashboard-Default-299ec2.svg" />
  </a>
  <a href="https://github.com/custom-components/hacs">
    <img src="https://img.shields.io/badge/HACS-Default-orange.svg" />
  </a>
  <a href="https://github.com/LRvdLinden/weather_dd_addon">
    <img src="https://img.shields.io/github/v/release/LRvdLinden/weather_dd_addon" />
  </a>
      <a href="https://github.com/LRvdLinden/weather_dd_addon">
    <img src="https://img.shields.io/github/downloads/LRvdLinden/weather_dd_addon/latest/total?color=purple&label=%20release%20Downloads" />
  </a>
    <a href="https://github.com/LRvdLinden/">
    <img src="https://img.shields.io/github/followers/LRvdLinden?style=social" />
  </a>
    </a>
    <a href="https://discord.gg/7yt64uX">
    <img src="https://img.shields.io/discord/688401603811999885" />
  </a>
</p>
<p align="center">Weather Dashboard in Home Assistant Dwains Dashboard.</p>


<p align="center">Created by <a href="https://github.com/LRvdLinden">Léon van der Linden</a>
</p> 


<p align="center">
  <img src="https://image.freepik.com/free-vector/weather-vector-banner_36298-522.jpg" />
</p>



## Prerequisite
---
- Make sure you have installed the lovelace [mini-graph-card](https://github.com/kalkih/mini-graph-card), [fontawesome icons](https://github.com/thomasloven/hass-fontawesome) and the [Neerslag app](https://github.com/aex351/home-assistant-neerslag-app). This can be done manually or directly via hacs

<img width="618" alt="image" src="https://user-images.githubusercontent.com/77990847/114733529-b6ca1a00-9d43-11eb-876a-6f4beda466ec.png">



## Make Home Assistant integration 
---
Please reboot Home Assistant after vonfig the sensors!

### Buienradar sensor + Radar map
- Make the integration with [Buienradar](https://www.home-assistant.io/integrations/sensor.buienradar/)
- Choose `latitude` and `longtiude` from the correct [weather station](https://www.google.com/maps/d/embed?mid=1NivHkTGQUOs0dwQTnTMZi8Uatj0&ll=52.92957401169076%2C5.184999999999995&z=7) 
 ```yaml
     # Example configuration.yaml entry
- platform: buienradar
  name: "Apeldoorn"
 # Force 'Meetstation Apeldoorn' to be used:
  latitude: 50.00
  longitude: 5.00
  monitored_conditions:
    - stationname
    - barometerfc
    - barometerfcname
    - conditioncode
    - condition
    - conditiondetailed
    - conditionexact
    - symbol
    - feeltemperature
    - humidity
    - temperature
    - groundtemperature
    - windspeed
    - windforce
    - winddirection
    - windazimuth
    - pressure
    - visibility
    - windgust
    - precipitation
    - irradiance
    - precipitation_forecast_average
    - precipitation_forecast_total
    - rainlast24hour
    - rainlasthour
      # conditions for forecasted data:
    - symbol_1d
    - symbol_2d
    - symbol_3d
    - symbol_4d
    - symbol_5d
    - temperature_1d
    - temperature_2d
    - temperature_3d
    - temperature_4d
    - temperature_5d
    - mintemp_1d
    - rainchance_1d
    - rainchance_2d
    - sunchance_1d
    - sunchance_2d
    - rain_1d
    - rain_2d
    - minrain_1d
    - maxrain_1d
    - windforce_1d
    - windforce_2d
    - windspeed_1d
    - windspeed_2d
    - winddirection_1d
    - winddirection_2d
    - windazimuth_1d
    - windazimuth_2d
```



 ```yaml
# Example configuration.yaml entry
camera:
  - platform: buienradar
```

### KMNI sensor
- Make the integration with [KNMI](https://www.home-assistant.io/integrations/scrape/)
 ```yaml
  - platform: scrape
    resource: https://www.knmi.nl/nederland-nu/weer/waarschuwingen/gelderland #change provincie
    select: "div.alert__heading"
    name: "knmi weercode"
    scan_interval: 300

  - platform: scrape
    resource: https://www.knmi.nl/nederland-nu/weer/waarschuwingen/gelderland #change provincie
    select: "a.alert__description"
    name: "knmi weer waarschuwing"
    scan_interval: 300    
```

### Moon sensor
- Make the integration with [Moon](https://www.home-assistant.io/integrations/moon/)
 ```yaml
  - platform: moon   
```

### Season sensor
- Make the integration with [Season](https://www.home-assistant.io/integrations/season/)
 ```yaml
  - platform: season  
```


- Install the the fronted lovelace [mini-graph-card](https://github.com/kalkih/mini-graph-card) from HACS or mannualy
- Install the the integration [Neerslag app](https://github.com/aex351/home-assistant-neerslag-app) from HACS or mannualy
- Reboot Home Assistant

## Installation Add-on
---
- Copy the `github` folder in to the `dwains-dashboard/addons/more_page` directory.
- Open your `more_page.yaml` file in `dwains-dashboard/configs` and add the following;
 ```yaml
     - name: Weather
       main_menu: 'true' #Show this addon in the main navigation bar!
       icon: fas:cloud-sun-rain
       path: 'dwains-dashboard/addons/more_page/weather/page.yaml'
```
- Reload the theme configuration via Theme Settings

## Replace the following
---
 ```yaml
   cards:
     - type: 'custom:github-flexi-card'
       title: Github LRvdLinden
       secondary_info: '{latest_release_tag}'
       url: true
       attribute_urls: true
       attributes:
         - views
         - stargazers
         - open_issues
         - clones
         - forks
         - open_pull_requests
      sort:
        - by: stargazers
        - by: views_unique
          ascending: true
      entities:
        - sensor.automations_dashboard_dwains_add_on
        - sensor.birthday_dwains_add_on
        - sensor.github_dwains_add_on
        - sensor.uptimerobot_dwains_add_on
        - sensor.uptimerobot_lovelace_card
```
- change `title` of the card
- add the correct `sensor` to monitor


## Options
---

![image](https://user-images.githubusercontent.com/8268674/97019224-fad42300-1547-11eb-8153-46c401f50455.png)

### Entity
| Name | Type | Default | Since | Description |
|:-----|:-----|:-----|:-----|:-----|
| entity | string | **(required)** | v0.1.0 | Entity ID e.g. `sensor.my_github_project`


### Entity Properties
| Name | Type | Default | Since | Description |
|:-----|:-----|:-----|:-----|:-----|
| name | [KString](#keywordstring) | `friendly_name` | v0.1.0 | Name override
| secondary_info | [KString](#keywordstring) |  | v0.1.0 | String to display underneath the entity name
| attributes | list([Attribute](#attribute)) |  | v0.1.0 | Attributes to display
| url | [KString](#keywordstring) \| bool |  | v0.2.0 | Url to open on click/tap. (when `true` is used the target url becomes repo homepage)
| attribute_urls | bool |  | v0.2.0 | When set to `true` turns on default urls for all the displayed attributes
| icon | string | `"mdi:github"` | v0.2.0 | Override for entity icon
| compact_view | bool | `true` | v1.0.0 | When set to `false` big icons (and values) are displayed

### Attribute
| Name | Type | Default | Since | Description |
|:-----|:-----|:-----|:-----|:-----|
| name | string | **(required)** | v0.1.0 | Name of the attribute
| icon | string |  | v0.1.0 | Icon override (there are default icons for most of the available attributes)
| url | [KString](#keywordstring) \| bool |  | v0.2.0 | Url to open on click/tap. (there are default urls for most of the available attributes, so you can just use `true`)
| label | [KString](#keywordstring) |  | v0.5.0 | Label/text which will be shown instead of the icon

### Sort options

| Name | Type | Default | Since | Description |
|:-----|:-----|:-----|:-----|:-----|
| by | string | **(required)** | v1.0.0 | Name of the attribute
| ascending | bool | `false` | v1.0.0 | Whether to sort ascending or descending

## Configuration examples
---

### Card

```yaml
type: 'custom:github-flexi-card'
title: Github projects
entities:
  - entity: sensor.github_dwains_add_on
    secondary_info: 'Released {latest_release_tag}'
    url: "{latest_release_url}" # url taken from attribute
    attributes:
      - name: views
        url: true # default url to graphs/traffic
      - name: stargazers
      - name: open_issues
      - name: clones
        url: "https://my.custom.url/path"
      - name: forks
      - name: open_pull_requests
        url: "{latest_open_pull_request_url}" # url taken from attribute
  - entity: sensor.hideseek_mod
    url: true # default url - repo homepage
    attributes:
      - views
      - stargazers
      - forks
  - entity: sensor.urleditorpro
    name: 'Url Editor Pro (v{latest_release_tag})'
    secondary_info: 'Clones: {clones}'
    attributes:
      - views
      - stargazers
      - open_issues
```

### Entity

Note: different type has to be used `custom:github-entity`

![image](https://user-images.githubusercontent.com/8268674/96303544-7be46500-0ff2-11eb-9a86-16af9c52f1d0.png)

```yaml
type: entities
title: Displayed as entity
show_header_toggle: false
entities:
  - sensor.home_assistant_v2_db
  - type: 'custom:github-entity'
    entity: sensor.github_dwains_add_on
    secondary_info: 'Released {latest_release_tag}'
    url: true
    attribute_urls: true
    attributes:
      - views
      - stargazers
      - open_issues
      - clones
      - forks
      - open_pull_requests
  - sensor.hassio_online
  - sensor.last_boot
  - sensor.processor_use
```

### Card-level entity properties

Card-level entity properties are useful when you want to have same settings for all of the entities.

![image](https://user-images.githubusercontent.com/8268674/96266114-30b05f00-0fbe-11eb-9d10-f9b9e5dfc1cf.png)

```yaml
type: 'custom:github-flexi-card'
title: Card-level entity properties
secondary_info: 'Released {latest_release_tag}'
url: true
attribute_urls: true
attributes:
  - views
  - stargazers
  - open_issues
  - clones
  - forks
  - open_pull_requests
entities:
  - sensor.battery_state_card
  - sensor.hideseek_mod
  - sensor.urleditorpro
```

### Labels instead of icons

![image](https://user-images.githubusercontent.com/8268674/96354074-37c49380-10ca-11eb-9151-829e5c37f877.png)

```yaml
type: 'custom:github-flexi-card'
title: Labels instead of icons
url: true
attribute_urls: true
attributes:
  - name: views
    label: Views
  - name: stargazers
    label: Stars
  - name: open_issues
    label: Issues
entities:
  - sensor.battery_state_card
  - sensor.hideseek_mod
  - sensor.urleditorpro
```

### Compact view (disabling)

![image](https://user-images.githubusercontent.com/8268674/96794344-eda71f00-13f5-11eb-85f2-f60caad2fa63.png)

```yaml
type: 'custom:github-flexi-card'
title: Big icons
url: true
attribute_urls: true
attributes:
  - views
  - stargazers
entities:
  - sensor.battery_state_card
  - entity: sensor.hideseek_mod
    compact_view: false
  - sensor.urleditorpro
```

### Sorting

![image](https://user-images.githubusercontent.com/8268674/96928429-72ef0a00-14b0-11eb-95dd-4f1c76e217ec.png)

```yaml
type: 'custom:github-flexi-card'
title: Sort by starts and views (asc)
secondary_info: '{latest_release_tag}'
url: true
attribute_urls: true
attributes:
  - views_unique
  - stargazers
  - open_issues
  - open_pull_requests
sort:
  - by: stargazers
  - by: views_unique
    ascending: true
entities:
  - sensor.battery_state_card
  - sensor.hideseek_mod
  - sensor.github_flexi_card
  - sensor.urleditorpro
  - entity: sensor.home_assistant_config
    secondary_info: null
```


## Result
---
![vd-weer](https://user-images.githubusercontent.com/77990847/114725586-e590c200-9d3c-11eb-8c2d-ad4bbd616815.png)



---
Enjoy my card? Help me out for a couple of :beers: or a :coffee:!

[![coffee](https://www.buymeacoffee.com/assets/img/custom_images/black_img.png)](https://www.buymeacoffee.com/LRvdLinden)
