# Yaml File Format

Since there will be a lot of different options, this file will break down how to format your games using [YAML](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html).

## Basic File Structure

In general, you should have a directory structure that looks like the following

```
my_game
  - enemies.yaml
  - rooms.yaml
  - items.yaml
  - player.yaml
  - config.yaml
```

Where `enemies.yaml` contains definitions for your enemies, `rooms.yaml` contains room definitions, and so on.


## Includes

If you have a large game, putting it all into the above files could make for some very large files. For this reason, we have added an include statement. By using include, you can write additional yaml files and include them in your main.

Here is an example enemies.yaml using includes only:

```yaml
include
  - weak_enemies.yaml
  - bosses/boss_1.yaml
  - bosses/boss_.yaml
```

This file simply contains a yaml list of all files to include. The included files will treated as if they are all one large file.

# Names

Enemies, rooms, and items all have unique names which can be used to refer to them in game (and in [item effects](Items.md#effects)). 

Because these names can be used to refer to specific objects, they must be unique; you can not have an enemy and item named the same thing. It is worth noting that names are not case-sensitive.  
Additionally, names must follow specific guidelines:

+ Start with alphabetic character or underscore
+ Be made up of only spaces, alphanumeric characters, and underscores
+ Any character after a space must not be numeric
+ Must not begin or end with spaces (they will be trimmed)
+ Any sequence of multiple spaces will be shortened to a single space

For example, `love potion`, `___`, `test12 test` are all valid names.  
`123 potion`, `sword 1`, `a,-b` are all invalid names.  
`love potion` and `love   potion` will be treated as identical.


## Min and Max Values

For properties which could be generated randomly, a range can be provided. This is done by replacing the property name with `min_<property>` and `max_<property>`.

**Example:** If the spider enemy has
```yaml
health: 10
```
it could be replaced with
```yaml
min_health: 5
max_health: 15
```
Now, instead of every spider enemy spawning with 10 health, they will be created with health varying between 5 and 15 points.


## Specific File & Object formats

Documentation on specific file formats can be found below:

* [Enemies](Enemies.md)
* [Rooms](Rooms.md)
* [Items](Items.md)
* [Player](Player.md)
* [Config](Config.yaml)
