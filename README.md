# Destiny Dynasty — Mod Releases

Distribución pública de JAR compilados de mods propios y versiones parcheadas.
El código privado permanece en sus repositorios de origen. No se suben fuentes,
credenciales, worlds ni configuraciones privadas del servidor.

## Publicar

Desde un checkout limpio y actualizado de este repositorio, PowerShell 7 y GitHub CLI:

```powershell
./tools/Publish-ModRelease.ps1 -RepositoryRoot . -ModId destiny-realms `
  -Version 0.1.1 -JarPath 'E:/destiny-realms/build/libs/destinydynasty-0.1.1.jar'
```

El ejemplo no representa una versión ya publicada. El script crea una release
`mod-destiny-realms-0.1.1`, publica un solo JAR y, tras verificar su SHA-256 y tamaño,
actualiza `channels/destiny-realms.json`. Nunca reemplaza una build publicada.

Cada mod tiene su propio canal; no debe utilizarse `/releases/latest` de este
repositorio compartido para actualizar un mod individual.

## Launcher

En una definición de variante del repositorio Modpack:

```json
{
  "path": "mods/destiny-realms.jar",
  "github": {
    "repository": "Destiny-Dynasty/Mod-Releases",
    "release": "latest",
    "channel": "destiny-realms",
    "asset": "destiny-realms-*.jar"
  }
}
```

El compositor añade la instantánea verificable al manifiesto schema 2. El launcher
consulta el canal al pulsar Jugar. Para fijar una build se usa su tag exacto en
`release`, sin `channel`. Publicar otro mod no cambia este canal.

## Automatización privada

Copiar `templates/publish-private-mod.yml` al repositorio privado y adaptar la
selección del JAR si el proyecto produce varios módulos. El secreto
`MOD_DISTRIBUTION_TOKEN` necesita Contents: write únicamente sobre Mod-Releases.
El token nunca se distribuye a jugadores. El workflow publica solo el binario.

## Compatibilidad y licencias

Publicar en un canal únicamente builds compatibles con su Minecraft, loader y
dependencias. Usar otro canal al mantener una línea incompatible. Los archivos
mantienen sus licencias y avisos originales. La licencia MIT de este repositorio
cubre las herramientas de publicación, no concede una licencia nueva a los JAR.

La primera build de Realms se importa del pack existente; no representa una
compilación nueva del HEAD privado.
