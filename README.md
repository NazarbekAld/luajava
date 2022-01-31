# nonlua #
[![License](https://img.shields.io/github/license/nondev/nonlua.svg)](http://opensource.org/licenses/MIT) 
[![Build Status](https://github.com/GuDzpoz/jua/actions/workflows/build-natives.yml/badge.svg)](https://github.com/GuDzpoz/jua/actions/workflows/build-natives.yml)

  * [About](#about)
  * [Quickstart](#quickstart)
  * [Java module](#java-module)
  * [Project template](#project-template)
  * [Credits](#credits)

## About ##

Jua is a scripting tool for Java. The goal of this tool is to allow scripts written in Lua to manipulate components developed in Java.

It allows Java components to be accessed from Lua using the same syntax that is used for accessing Lua`s native objects, without any need for declarations or any kind of preprocessing. Nonlua also allows Java to implement an interface using Lua. This way any interface can be implemented in Lua and passed as parameter to any method, and when called, the equivalent function will be called in Lua, and it's result passed back to Java.

## Quickstart ##

To include Nonlua into your project, you can use Maven or Gradle. Artifacts (yet to be):

* Core: `party.iroiro.jua:jua:2.1.0-beta3-alpha-1`
* Desktop natives: `party.iroiro.jua:jua-platform:2.1.0-beta3-alpha-1:natives-desktop`

And here is simple example on how to correctly initialize new Lua instance.
This example will push `message` variable to Lua with value `Hello World from Lua`, then prints it using Lua built-in `print` function.

```java
Lua.files = new DesktopFiles();
Lua L = new Lua();

L.push("Hello World from Lua");
L.set("message");
L.run("print(message)");

L.dispose();
```

### Java module ###

Example on how to use `java` module in Lua to create basic LibGDX application:

```lua
local Gdx = java.require("com.badlogic.gdx.Gdx")
local GL20 = java.require("com.badlogic.gdx.graphics.GL20")
local SpriteBatch = java.require("com.badlogic.gdx.graphics.g2d.SpriteBatch")
local Texture = java.require("com.badlogic.gdx.graphics.Texture")

local batch, img

function create()
  batch = java.new(SpriteBatch)
  img = java.new(Texture, "badlogic.jpg")
end

function render()
  Gdx.gl:glClearColor(1, 0, 0, 1)
  Gdx.gl:glClear(GL20.GL_COLOR_BUFFER_BIT)

  batch:begin()
  batch:draw(img, 0, 0)
  batch:end()
end

function dispose()
  batch:dispose()
  img:dispose()
end
```

## Credits ##

 * [LuaJava](https://github.com/jasonsantos/luajava)
 * [LibGDX](https://github.com/libgdx/libgdx)
 * [Nonlua](https://github.com/deathbeam/jua)
 
Nonlua is based on LuaJava. So all thanks to Jason Santos for his awesome work on it.