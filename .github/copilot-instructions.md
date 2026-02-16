# Copilot Instructions for tpl-lambda-python

## Arquitectura y componentes principales
- **Función principal:** Toda la lógica está en `src/lambda_function.py`.
- **Infraestructura:** Definida en `template.yml` usando AWS SAM (Serverless Application Model). Aquí se configuran Lambda, API Gateway, variables de entorno y eventos.
- **Configuración por ambiente:** Archivos en `config/` (ej: `dev.yml`, `prod.yml`) para separar settings según entorno.
- **Eventos de prueba:** Carpeta `events/` con ejemplos de payloads para pruebas locales.
- **Pruebas unitarias:** En `tests/`, usando Pytest.

## Flujos de trabajo críticos
- **Desarrollo local y pruebas:**
  - Usa el devcontainer (VS Code) para entorno preconfigurado.
  - Levanta la API localmente con `sam local start-api`.
  - Invoca la Lambda localmente con `sam local invoke LambdaFunction --event events/apigateway-aws-proxy.json`.
- **Instalación de dependencias:**
  - Ejecuta `pip install -r requirements-dev.txt` si agregas nuevas librerías.
- **Construcción y despliegue:**
  - `sam build` para compilar.
  - `sam validate` para validar la plantilla.
  - `sam deploy --guided` para desplegar **solo en ambientes locales o cuentas sandbox**. El aprovisionamiento de infraestructura real (dev, prod) se realiza exclusivamente mediante **Terraform** fuera de este repositorio.
- **Logs y limpieza:**
  - `sam logs -n LambdaFunction` para logs.
  - `sam delete` para eliminar recursos de AWS.

## Convenciones y patrones del proyecto
- **Commits:** Usar siempre el estándar **conventional-commits** para los mensajes de commit.
- **Pull Requests:** Las descripciones de los PRs deben estar redactadas en **español**.
- **Handler Lambda:** Siempre en `src/lambda_function.py`, función `lambda_handler`.
- **Configuración:** No hardcodear settings; usar archivos en `config/` y variables de entorno.
- **Eventos:** Generar ejemplos con `sam local generate-event ...` y guardarlos en `events/`.
- **Pruebas:** Usar Pytest, archivos de test en `tests/`.
- **Infraestructura:** No modificar recursos críticos en `template.yml` sin validación previa.

## Integraciones y dependencias
- **AWS SAM CLI:** Esencial para desarrollo, pruebas y despliegue.
- **Terraform:** El despliegue a ambientes productivos se realiza fuera de este repo, vía Terraform.
- **Devcontainer:** Facilita la configuración homogénea del entorno de desarrollo.

## Archivos clave
- `src/lambda_function.py`: Lógica principal.
- `template.yml`: Infraestructura y eventos.
- `config/`: Configuración por ambiente.
- `events/`: Ejemplos de eventos.
- `tests/`: Pruebas unitarias.

---

> Si algún flujo, convención o integración no está claro, consulta el README.md o pregunta para mejorar estas instrucciones.
