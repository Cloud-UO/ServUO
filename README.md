# CloudUO

A cloud-ready dev environment, hosting framework and toolset for Ultima Online server emulators, primarily ServUO.

## Requirements

- Docker
- Docker Compose
- Ultima Online Client Files

## Installation

Copy your Ultima Online client files into the folder `client`.

```bash
docker create network clouduo
```

## VS Code Server Included

Edit your shard files in any browser.  You also get full access to your shard's terminal.

After the stack is up, your editor is available at http://localhost:8443.

Feel free to then install your own extensions,  such as C#, within the browser window.

---
## Quick Create a Shard

```bash
 git clone https://github.com/Cloud-UO/clouduo.git cloud && cd cloud
 ```

 Edit `.env`

 ```bash
 docker-compose up -d
```

On the first launch, give the box a moment to become available to your UO client.  It will be building ServUO from source and may take just a moment.

---
## Connect To Your Shard

Shard will be available at 127.0.0.1 and whichever port you specified in `.env`


---
## Using Your Own Shard Files

Place your shard files into folder `shard`, and the build image will copy it over.

---
## Entire Shard Folder Not Needed

Since it is using data layering technology, we can do as little as adding an override file for CharacterCreation.cs.

#### Overriding Single Files

It is important to note, when mounting a single file, rather than a directory, the file must exist on the host.  A solid note on that is that docker will try to mount the location as a folder that doesn't exist, and you'll end up with weird empty folders everywhere.

```bash
volumes:
    - ./overrides/Misc/AutoSave.cs:/shard/Scripts/Misc/AutoSave.cs
```

If this were the only volume you mounted, your saves would not persist, but it would be a full functional and running ServUO server with a modded AutoSave.cs.

The image will build your file on top of the initial image build, without ever changing or modifying it's base.

---


Basically...we'll be able to not only do things like script releasese, but entire server templating, and we're talking about in an instance.  We can spawn a hundred shards at once, and turn them off during times of unused.  We can play single player Ultima Online with admin abilities ready to go in a couple of commands.

We can run 3 shards at once, based on the same shard folder, but mounted with different save folders (awesome for running a side by side TC and your production environment from one place).


#### Mount a Folder

```bash
volumes:
    - ./shard/scripts:/shard/Scripts
```

## Future Plugins (packs) Planned

- Digital Ocean Spaces Integration

- Digital Ocean Auto Deployment

- docl

- GitLab CE

- Pre-AOS Server Pack

- Custom Scripts as Plugins
