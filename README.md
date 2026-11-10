# TP 4 — Integración Continua / DevSecOps

API Express y pipeline de GitHub Actions, basados en el proyecto de referencia compartido y en la guía de la cátedra. El archivo corregido `pipeline.yml` entregado por el docente coincide con los controles base usados aquí. Se incluyen Trivy y ZAP como extras.

## Ejecutar

```bash
npm ci
npm test
node app.js
```

API: `http://localhost:3000/total?p=10&c=2` devuelve `{"total":20}`. `/calcular?a=2&b=3` devuelve `{"resultado":5}`.

## Controles

| Control | Herramienta | Objetivo |
|---|---|---|
| Tests | node:test | Fórmula de descuento |
| SCA | npm audit | Dependencias vulnerables |
| SAST | Semgrep, config auto | Código inseguro |
| Secretos | Gitleaks | Código e historial del PR |
| Configuración | Trivy | Dockerfile |
| DAST | ZAP baseline | App ejecutándose |

El workflow está en `.github/workflows/pipeline.yml` y se dispara al abrir o actualizar un pull request. El código final incluye Helmet, usuario no privilegiado en Docker y una exclusión documentada de la alerta informativa 10049 de ZAP.

## Parte que se debe realizar en GitHub

No hay todavía PR propios ni ejecuciones de Actions verificadas para este repositorio. Los resultados del proyecto de referencia no cuentan como evidencia de esta entrega.

La publicación se deja para una etapa posterior por indicación de la alumna.

1. Publicar este repositorio en una cuenta personal y conectar el remoto.
2. Abrir un PR para comprobar el pipeline base.
3. Crear cuatro ramas separadas desde main: secreto ficticio con formato de token, ruta con `eval`, dependencia `lodash@4.17.15` y fórmula `(1 + desc)`. Seguir los valores y pasos exactos de la guía de cátedra. Nunca utilizar una clave real.
4. Guardar enlaces o capturas de los controles que fallen.
5. Corregir las ramas de código, dependencia y fórmula y verificar que vuelvan a verde. Cerrar sin fusionar la del secreto: borrarlo del último archivo no lo quita del historial.
6. En Settings → Rules, exigir el check `verificar` para fusionar en main y comprobar el bloqueo con un PR fallido.
7. Verificar también Trivy y ZAP.

## Explicación para la defensa

SCA revisa bibliotecas; SAST inspecciona código sin ejecutarlo; DAST prueba el servicio en ejecución. Gitleaks busca secretos, y el test comprueba el cálculo. Cada control detecta una clase diferente de falla. Tener un workflow en el repositorio no basta: las ejecuciones y los PR deben quedar registrados en GitHub.
