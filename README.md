# Web Exploitation

### Comandos útiles para explotación web y pruebas de seguridad

---

## **Escaneo agresivo con Nmap**

```
nmap <opciones> <objetivo> -o <archivo_salida>
```

### **Parámetros y ejemplos:**
- `-sC`: Ejecuta los scripts de detección predeterminados.
- `-sV`: Detecta versiones de los servicios en los puertos abiertos.
- `-A`: Activa la detección de sistema operativo, versión de servicio, scripts y traceroute.
- `-T<n>`: Ajusta la velocidad de escaneo (de 0 a 5, donde 5 es el más rápido). Ejemplo: `-T5`
- `-n`: No resuelve nombres de dominio (evita consultas DNS).
- `-Pn`: Trata todos los hosts como si estuvieran activos (ignora respuestas ICMP).
- `-p <puertos>`: Especifica los puertos a escanear (Ejemplo: `-p 22,80`).
- `-o <archivo_salida>`: Guarda el resultado en un archivo (Ejemplo: `-o aggressiveScan.txt`).

**Ejemplo de uso:**
```
nmap -sC -sV -A -T5 -n -Pn -p 22,80 10.10.11.44 -o aggressiveScan.txt
```
---

## **Escaneo de directorios con FeroxBuster**

```
feroxbuster -u <url> -w <lista_palabras> <opciones>
```

### **Parámetros y ejemplos:**
- `-u <url>`: Especifica la URL objetivo (Ejemplo: `-u http://target.com`).
- `-w <lista_palabras>`: Usa una lista de palabras para encontrar directorios y archivos ocultos (Ejemplo: `-w /usr/share/wordlists/dirbuster.txt`).
- `-t <n>`: Usa `n` hilos para el escaneo (Ejemplo: `-t 50`).
- `-r`: Sigue redirecciones.
- `--scan-dir-listings`: Busca listados de directorios abiertos.

**Ejemplo de uso:**
```
feroxbuster -u http://target.com -w /usr/share/wordlists/dirbuster.txt -t 50 -r --scan-dir-listings
```

---

## **Fuzzing de subdominios con FFUF**

```
ffuf -u <url> -H "Host: FUZZ.<url>" -w <lista_palabras> <opciones>
```

### **Parámetros y ejemplos:**
- `-u <url>`: URL base del objetivo (Ejemplo: `-u http://alert.htb`).
- `-H "Host: FUZZ.<url>"`: Utiliza "FUZZ" como marcador en la cabecera `Host` para buscar subdominios.
- `-w <lista_palabras>`: Especifica la lista de palabras a usar (Ejemplo: `-w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt`).
- `-t <n>`: Define el número de hilos (Ejemplo: `-t 200`).
- `-ac`: Activa la detección automática de respuestas similares para evitar falsos positivos.

**Ejemplo de uso:**
```
ffuf -u http://alert.htb -H "Host: FUZZ.alert.htb" -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -t 200 -ac
```

---

## **Extracción de datos con SQLMap**

```
sqlmap -u <url> <opciones>
```

### **Parámetros y ejemplos:**
- `-u <url>`: Especifica la URL a analizar (Ejemplo: `-u "http://target.com/page?id=1"`).
- `--dbs`: Enumera las bases de datos disponibles.
- `-D <database> --tables`: Muestra las tablas de una base de datos específica.
- `-D <database> -T <table> --dump`: Extrae los datos de una tabla específica.

**Ejemplo de uso:**
```
sqlmap -u "http://target.com/page?id=1" --dbs
sqlmap -u "http://target.com/page?id=1" -D users --tables
sqlmap -u "http://target.com/page?id=1" -D users -T credentials --dump
```

---

## **Envío de peticiones con cURL**

```
curl <opciones> <url>
```

### **Parámetros y ejemplos:**
- `-X <método>`: Especifica el método HTTP a usar (Ejemplo: `-X POST`).
- `-H "Header: valor"`: Agrega una cabecera personalizada (Ejemplo: `-H "User-Agent: Firefox"`).
- `-d "data"`: Envía datos en una petición (Ejemplo: `-d "username=admin&password=1234"`).

**Ejemplo de uso:**
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "username=admin&password=1234" http://target.com/login
```

---
