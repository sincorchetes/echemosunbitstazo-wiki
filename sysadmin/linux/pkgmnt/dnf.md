# DNF

## Gestión de paquetería

### Refrescar la base de datos de DNF

```bash
dnf check-update
```

### Actualizar el sistema con los últimos parches

```bash
dnf upgrade
```

### Sincronizar los últimos paquetes instalados

NOTA: Solo cuando se actualiza de versión.

```bash
dnf distro-sync
```

### Instalar software

```bash
dnf install [paquete1 paquete2...]
```

### Desinstalar software

```bash
dnf remove [paquete1 paquete2...]
```

### Buscar software

```bash
dnf search [palabra_a_buscar]
```

### Buscar paquetes mediante un archivo

```bash
dnf provides /bin/bash
```

### Descargar solo paquetes

```bash
dnf download [paquete1 paquete2...]
```

### Obtener información del paquete

```bash
dnf info [paquete]
```

## Interactuando con módulos

