## Mappings for Logitech F310

![](image.jpg)

This is a configuration that can be applied to a `Logitech F310`:

![](controller.jpg)

This is meant for controlling a linux system.

Can be suitable for light browsing or navigation.

It works through [input-remapper](https://github.com/sezanzeb/input-remapper):

![](input_remapper.jpg)

There's an `AUR` package [here](https://aur.archlinux.org/packages/input-remapper-git).

Remember to `sudo systemctl start input-remapper` after installation.

Then launch `input-remapper-gtk` in a terminal.

---

The `json` file should be placed here:

 `~/.config/input-remapper-2/presets/Logitech Gamepad F310`

---

## Configuration

This is the current configuration but you can change it as you see fit.

It includes some shortcuts I use in my `wm` which might not be relevant to yours.

---

**Stick Left:** Move mouse cursor

**Stick Right:** Vertical and horizontal wheel scrolling

---

**Button Left:** Click

**Button Down:** Right Click

**Button Up:** Middle Click

**Button Right:** Mod Button (See below)

---

**Pad Left:** Audio Prev

**Pad Right:** Audio Next

**Pad Up:** Volume Up

**Pad Down:** Volume Down

---

**Top Left:** Previous Tag

**Top Right:** Next Tag

---

**Trigger Left:** Go To Top under cursor

**Trigger Right:** Go To Bottom under cursor

Functions in my `wm` look like:

```lua
function Utils.home_on_cursor()
  local c = mouse.object_under_pointer()

  if c then
    Utils.focus(c)
    Utils.fake_input_do(true, false, false, "Home")
  end
end

function Utils.end_on_cursor()
  local c = mouse.object_under_pointer()

  if c then
    Utils.focus(c)
    Utils.fake_input_do(true, false, false, "End")
  end
end
```

---

**Thumb Left:** Move cursor to next screen

In my `wm` this places the cursor on the next screen to the right and places it at the center.

This is useful to fast-travel instead of moving the cursor with the stick all the way there.

It wraps when it reaches the last screen.

The functions in my `wm` look like this:

```lua
function Utils.center_cursor()
  local screen = Utils.my_screen()
  local workarea = screen.workarea

  mouse.coords({
    x = workarea.x + workarea.width / 2,
    y = workarea.y + workarea.height / 2,
  })
end

function Utils.cursor_on_next_screen()
  awful.screen.focus_relative(1)
  Utils.center_cursor()
end
```

---

**Thumb Right:** Refresh (F5) under cursor

Functions in my `wm` look like:

```lua
function Utils.refresh_on_cursor()
  local c = mouse.object_under_pointer()

  if c then
    Utils.focus(c)
    Utils.fake_input_do(false, false, false, "F5")
  end
end
```

---

**Select:** Play/Pause music

**Start:** Lock screen

**Big Button:** Toggle maximize on window under cursor

The functions in my `wm` look like this:

```lua
function Utils.maximize(c)
  c.maximized = not c.maximized
  Utils.focus(c)
end

function Utils.maximize_on_cursor(c)
  local c = mouse.object_under_pointer()

  if c then
    Utils.maximize(c)
  end
end
```

---

## Mod Button

`Button Right` is a button that can be used with other buttons for further mappings.

I'll refer to it as `Mod`.

---

**Mod + Pad Up:** Zoom In

**Mod + Pad Down:** Zoom Out

**Mod + Pad Left:** Go Back

**Mod + Pad Right:** Go Forward

**Mod + Top Left:** Esc Key

**Mod + Stick Left:** Faster cursor movement (Turbo)

**Mod + Big Button:** Close application under cursor

The function in my `wm` looks similar to:

```lua
function Utils.close_on_cursor(c)
  local c = mouse.object_under_pointer()

  if c then
    c:kill()
  end
end
```

---

## Hints

If `input-remapper` is not detecting the device after installation, try re-plugging the controller and restart the program.

`input-remapper-gtk` might periodically stop working while you're editing buttons because it loses root access, you're supposed to input the password again in the terminal where you run it.

`input-remapper-gtk` shows important information in the footer at the bottom.