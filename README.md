# templated_scene

A Home Assistant custom component to template scenes.

## Install

:warning: Don't, yet. This is a WIP.

### Manually

Copy the contents of `templated_scene` into your Home Assistant's `custom-components` folder.

### Automatically with HACS

Coming later.

## Configure

Add the component `templated_scene` to your configuration and scenes like you're used to ([documentation](https://www.home-assistant.io/integrations/scene/)), except you are now able to template ([documentation](https://www.home-assistant.io/docs/configuration/templating/)) any field you set.

### Example configuration

```yaml
templated_scene:
  - name: Lights
    entities:
      light.living_room_spots:
        state: on
        brightness: "{{ 255 if is_state('group.everyone', 'home') else 0 }}"
        color_temp: "{{ 475 if is_state('sensor.time_of_day', 'evening') else 350 }}"
```

This will create `scene.lights`, which will be re-applied every time a dependency (`group.everyone` and `sensor.time_of_day` in this case) changes. Note the use of `brightness: 0` to turn the light off.

## To do

- [ ] Duplicate implementation for `scene` in core as much as possible with regards to configuration
- [ ] Upon loading of the integration, "create" the scenes (don't actually save them as entities), and try to apply them (no support for templates yet)
- [ ] Add support for templates (render right before applying)
- [ ] Subscribe to the template, and re-apply every time it rerenders
