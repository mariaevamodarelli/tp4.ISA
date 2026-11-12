# Verificación — 10 de noviembre de 2026

## Verificado localmente

- `npm ci`: correcto.
- `npm test`: 1 test, 1 aprobado.
- `npm audit --audit-level=high`: sin vulnerabilidades reportadas.
- API en puerto 3000: `/total?p=10&c=2` devolvió 20 y `/calcular?a=2&b=3` devolvió 5.
- Headers `X-Content-Type-Options: nosniff` y `Cache-Control: no-store`: presentes. Ruta inexistente: 404.
- Trivy 0.75.0, `config --exit-code 1 --severity HIGH,CRITICAL`: sin hallazgos de configuración en Dockerfile. Este comando no es un escaneo de CVE de la imagen.

- ZAP baseline contra `/total?p=10&c=2`: 67 comprobaciones aprobadas, 0 FAIL y 0 WARN de seguridad; alerta informativa 10049 ignorada según `.zap/rules.tsv`. Reportes en `evidencias/zap.html` y `evidencias/zap.json`. El plan avisó que `/` devolvió 404 (la API no define una portada).
