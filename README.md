[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/custom-components/hacs)
![Version](https://img.shields.io/github/v/release/Petro31/easy-time-jinja)
![Downloads](https://img.shields.io/github/downloads/Petro31/easy-time-jinja/total)

<a href="https://www.buymeacoffee.com/Petro31"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=Petro31&button_colour=5F7FFF&font_colour=ffffff&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00" /></a>

# Easy Time

Tired of getting help performing math with time?  Look no further.  This Template extension for home assistant makes time easy calculations easy!

# Installation

Install this in HACS or download the `easy_time.jinja` from this repository and place the files into your `config\custom_templates` directory.

After installation, you can edit the first line to set a default language, this will make the macros easier to use in your native language.

```
{%- set default_language = 'en' %}
```

# Easy Relative Time Macros

Looking for times in the future or the past in your language?  Look no further.  These easy macros will pave the way to the future...

## `easy_time(entity_id_or_time)`

`easy_time` returns the most significant friendly relative time.  For example, if your uptime is 3 hours, 2 minutes, and 1 second, this macro will return `3 hours` in your default language.

Arugment | Type | Default | Example | Description
:-:|:-:|:-:|:-:|---
entity_id_or_time| string, datetime, or entity_id | - | `'sensor.uptime'` | (Required) The entity_id, date string, or datetime object.
attribute| str or None | No | `None` | (Optional) attribute to extract the desired time from.
language| string | set by user | `'en'` | (Optional) Override the default language.
utc| boolean | `False` | `True` | (Optional) If your `uptime` argument does not have a timezone and you wish to treat it as a UTC timestamp, set this to True.  Otherwise the function assumes `Local` calculations.

### Examples

```jinja
{% from 'easy_time.jinja' import easy_time %}

{# From an entity state #}
{{ easy_time('input_datetime.alarm_time') }}

{# Last Updated #}
{{ easy_time(states.sensor.my_energy_meter.last_updated) }}

{# Calendar entity attribute #}
{{ easy_time('calendar.my_events', 'start_time') }}

{# Overriding language or utc entity attribute #}
{{ easy_time("2023-04-07 00:00:00", 'en', True) }}
{{ easy_time("2023-04-07 00:00:00", language='en', utc=True) }}
{{ easy_time('calendar.my_events', 'start_time', 'en', True) }}
{{ easy_time('calendar.my_events', 'start_time', language='en', utc=True) }}
```

## `big_time(entity_id_or_time)`

`big_time` returns the friendly relative time without missing any details.  For example, if your uptime is 3 hours, 2 minutes, and 1 second, this macro will return `3 hours, 2 minutes, and 1 second` in your default language.

Arugment | Type | Default | Example | Description
:-:|:-:|:-:|:-:|---
entity_id_or_time| string, datetime, or entity_id | - | `'sensor.uptime'` | (Required) The entity_id, date string, or datetime object.
attribute| str or None | No | `None` | (Optional) attribute to extract the desired time from.
language| string | set by user | `'en'` | (Optional) Override the default language.
utc| boolean | `False` | `True` | (Optional) If your `uptime` argument does not have a timezone and you wish to treat it as a UTC timestamp, set this to True.  Otherwise the function assumes `Local` calculations.

### Examples

```jinja
{% from 'easy_time.jinja' import big_time %}

{# From an entity state #}
{{ big_time('input_datetime.alarm_time') }}

{# Last Updated #}
{{ big_time(states.sensor.my_energy_meter.last_updated) }}

{# Calendar entity attribute #}
{{ big_time('calendar.my_events', 'start_time') }}

{# Overriding language or utc entity attribute #}
{{ big_time("2023-04-07 00:00:00", 'en', True) }}
{{ big_time("2023-04-07 00:00:00", language='en', utc=True) }}
{{ big_time('calendar.my_events', 'start_time', 'en', True) }}
{{ big_time('calendar.my_events', 'start_time', language='en', utc=True) }}
```

## `custom_time(entity_id_or_time, values)` and `custom_time_attr(entity_id, attribute, values)`

`custom_time` and `custom_time_attr` returns the friendly relative time providing detials that are to your needs... most of the time.  For example, if your uptime is 3 hours, 2 minutes, and 1 second, this macro will return `3 hours and 2 minutes` in your default language.

Arugment | Type | Default | Example | Description
:-:|:-:|:-:|:-:|---
uptime| string, datetime, or entity_id | - | `'sensor.uptime'` | (Required) The entity_id, date string, or datetime object.
attribute| str or None | No | `None` | (Required for `custom_time_attr`) attribute to extract the desired time from.
values | string | none | `'day, hour, minute'` | (Required) Options for displaying time.  Available options: `year`, `week`, `day`, `hour`, `minute` and `second`. 
language| string | set by user | `'en'` | (Optional) Override the default language.
utc| boolean | `False` | `True` | (Optional) If your `uptime` argument does not have a timezone and you wish to treat it as a UTC timestamp, set this to True.  Otherwise the function assumes `Local` calculations.

### Examples

```jinja
{% from 'easy_time.jinja' import custom_time, custom_time_attr %}

{# From an entity state #}
{# NOTE: the value after the = sign for minute and hour can be anything. #}
{{ custom_time('input_datetime.alarm_time', hour=1, minute=1) }}

{# Calendar entity attribute #}
{{ custom_time_attr('calendar.my_events', 'start_time', hour=1, minute=1) }}

{# Last Updated #}
{{ custom_time(states.sensor.my_energy_meter.last_updated, hour=1, minute=1) }}

{# Overriding language or utc entity attribute #}
{{ custom_time("2023-04-07 00:00:00", 'hour', 'minute', language='en', utc=True) }}
{{ custom_time_attr('calendar.my_events', 'start_time', 'hour', 'minute', language='en', utc=True) }}
```

## `easy_relative_time(entity_id_or_time)`

`easy_relative_time` returns the most significant friendly relative time.  For example, if your uptime is 3 hours, 2 minutes, and 1 second, this macro will return `in 3 hours` or `3 hours ago` in your default language.

Arugment | Type | Default | Example | Description
:-:|:-:|:-:|:-:|---
uptime| string, datetime, or entity_id | - | `'sensor.uptime'` | (Required) The entity_id, date string, or datetime object.
attribute| str or None | No | `None` | (Optional) attribute to extract the desired time from.
language| string | set by user | `'en'` | (Optional) Override the default language.
utc| boolean | `False` | `True` | (Optional) If your `uptime` argument does not have a timezone and you wish to treat it as a UTC timestamp, set this to True.  Otherwise the function assumes `Local` calculations.

### Examples

```jinja
{% from 'easy_time.jinja' import easy_relative_time %}

{# From an entity state #}
{{ easy_relative_time('input_datetime.alarm_time') }}

{# Last Updated #}
{{ easy_relative_time(states.sensor.my_energy_meter.last_updated) }}

{# Calendar entity attribute #}
{{ easy_relative_time('calendar.my_events', 'start_time') }}

{# Overriding language or utc entity attribute #}
{{ easy_relative_time("2023-04-07 00:00:00", 'en', True) }}
{{ easy_relative_time("2023-04-07 00:00:00", language='en', utc=True) }}
{{ easy_relative_time('calendar.my_events', 'start_time', 'en', True) }}
{{ easy_relative_time('calendar.my_events', 'start_time', language='en', utc=True) }}
```

## `big_relative_time(entity_id_or_time)`

`big_relative_time` returns the friendly relative time without missing any details.  For example, if your uptime is 3 hours, 2 minutes, and 1 second, this macro will return `in 3 hours, 2 minutes and 1 second` or `3 hours, 2 minutes and 1 second ago` in your default language.

Arugment | Type | Default | Example | Description
:-:|:-:|:-:|:-:|---
uptime| string, datetime, or entity_id | - | `'sensor.uptime'` | (Required) The entity_id, date string, or datetime object.
attribute| str or None | No | `None` | (Optional) attribute to extract the desired time from.
language| string | set by user | `'en'` | (Optional) Override the default language.
utc| boolean | `False` | `True` | (Optional) If your `uptime` argument does not have a timezone and you wish to treat it as a UTC timestamp, set this to True.  Otherwise the function assumes `Local` calculations.

### Examples

```jinja
{% from 'easy_time.jinja' import big_relative_time %}

{# From an entity state #}
{{ big_relative_time('input_datetime.alarm_time') }}

{# Last Updated #}
{{ big_relative_time(states.sensor.my_energy_meter.last_updated) }}

{# Calendar entity attribute #}
{{ big_relative_time('calendar.my_events', 'start_time') }}

{# Overriding language or utc entity attribute #}
{{ big_relative_time("2023-04-07 00:00:00", 'en', True) }}
{{ big_relative_time("2023-04-07 00:00:00", language='en', utc=True) }}
{{ big_relative_time('calendar.my_events', 'start_time', 'en', True) }}
{{ big_relative_time('calendar.my_events', 'start_time', language='en', utc=True) }}
```

## `custom_relative_time(entity_id_or_time, values)` and `custom_relative_time_attr(entity_id, attribute, values)`

`custom_relative_time` and `custom_relative_time_attr` returns the friendly relative time providing detials that are to your needs... most of the time.  For example, if your uptime is 3 hours, 2 minutes, and 1 second, this macro will return `3 hours and 2 minutes` in your default language.

Arugment | Type | Default | Example | Description
:-:|:-:|:-:|:-:|---
uptime| string, datetime, or entity_id | - | `'sensor.uptime'` | (Required) The entity_id, date string, or datetime object.
attribute| str or None | No | `None` | (Required for `custom_relative_time_attr`) attribute to extract the desired time from.
values | string | none | `'day, hour, minute'` | (Required) Options for displaying time.  Available options: `year`, `week`, `day`, `hour`, `minute` and `second`. 
language| string | set by user | `'en'` | (Optional) Override the default language.
utc| boolean | `False` | `True` | (Optional) If your `uptime` argument does not have a timezone and you wish to treat it as a UTC timestamp, set this to True.  Otherwise the function assumes `Local` calculations.

### Examples

```jinja
{% from 'easy_time.jinja' import custom_relative_time, custom_relative_time_attr %}

{# From an entity state #}
{{ custom_relative_time('input_datetime.alarm_time', 'hour, minute') }}

{# Last Updated #}
{{ custom_relative_time(states.sensor.my_energy_meter.last_updated, 'hour, minute') }}

{# Calendar entity attribute #}
{{ custom_relative_time_attr('calendar.my_events', 'start_time', 'hour, minute') }}

{# Overriding language or utc entity attribute #}
{{ custom_relative_time("2023-04-07 00:00:00", 'hour, minute', language='en', utc=True) }}
{{ custom_relative_time_attr('calendar.my_events', 'start_time', 'hour, minute', language='en', utc=True) }}
```

# Easy Date Macros

These macros create iso formatted date strings that can easily be turned into datetime objects.


## Arguments for each macro

<table>
<tr><td valign="Top">

month | number
:-:|:-:
January | 1
February | 2
March | 3
April | 4
May | 5
June | 6
July | 7
August | 8
September | 9
October | 10
November | 11
December | 12

</td><td valign="Top">

week | number
:-:|:-:
1st | 1
2nd | 2
3rd | 3
4th | 4
5th | 5
6th | 6

</td><td valign="Top">

day | number
:-:|:-:
Monday|0
Tuesday|1
Wednesday|2
Thursday|3
Friday|4
Saturday|5
Sunday|6
</td></tr> </table>

## `month_week_day(month, week, day)`

This macro will return the nth day in the nth week of a month.  This is best used to get the 2nd tuesday of any month, or the Thanksgiving American Holiday!

### Examples

```jinja
{% from 'easy_time.jinja' import month_week_day %}

{# Thanksgiving as a iso string #}
{{ month_week_day(11, 4, 3) }} 

{# Thanksgiving as a datetime for math#}
{{ month_week_day(11, 4, 3) | as_datetime }} 

{# 2nd sunday in January as an ios string #}
{{ month_week_day(1, 2, 2) }} 

{# 2nd sunday in January as a datetime #}
{{ month_week_day(1, 2, 2) | as_datetime }} 
```

## `month_day(month, week, day)`

This macro will return the nth day in the nth week of a month.  This is best used to get the 2nd tuesday of any month, or the Thanksgiving American Holiday!

### Examples

```jinja
{% from 'easy_time.jinja' import month_day %}

{# 4th of july #}
{{ month_day(7, 4) }} 
{{ month_day(7, 4) | as_datetime }} 
```

## `last_day_in_month(month, day)`

This macro will return the last day in a moth.  Do you ever want the last Sunday of each month?  Look no futhur.

### Examples

```jinja
{% from 'easy_time.jinja' import last_day_in_month %}

{# Last Sunday in August #}
{{ last_day_in_month(8, 6) }} 
{{ last_day_in_month(8, 6) | as_datetime }} 
```

## `easter()`

Apparently easter falls on a different sunday ever year and it takes a small army to figure it out.

### Examples

```jinja
{% from 'easy_time.jinja' import easter %}

{# Last Sunday in August #}
{{ easter() }} 
{{ easter() | as_datetime }} 
```

# Easy Daylight Savings

Ever wonder if you're falling behind or jumping ahead?  Want to be notified a week before daylight savings?  These templates will help with that.

## `next_dst()`

Returns an iso formatted time string of the exact minute the next DST goes into affect.

### Examples

```jinja
{% from 'easy_time.jinja' import next_dst %}

{# Next daylight savings time #}
{{ next_dst() }} 
{{ next_dst() | as_datetime }} 
```

## `next_dst_phrase()`

Want a friendly phrase telling you whether you will gain or lose time?  `gain 1 hour` or `lose 1 hour`

### Examples

```jinja
{% from 'easy_time.jinja' import next_dst_phrase %}

{# Next daylight savings time #}
{{ next_dst_phrase() }} 
{{ next_dst_phrase() | as_datetime }} 
```

## `days_until_dst()`

This outputs the number of days until the next DST.  Useful for notifications.  When the number of days is 7, send a notification.  "You will gain 1 hour in 7 days"

### Examples

```jinja
{% from 'easy_time.jinja' import days_until_dst %}

{# Next daylight savings time #}
{{ days_until_dst() }} 
{{ days_until_dst() | int }}
```
