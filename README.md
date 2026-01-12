# URL Change Detection con urlwatch

Monitoreo automático de cambios en páginas web usando GitHub Actions.

## 🚀 Setup Rápido

### 1. Crear el repositorio

```bash
# Crea un nuevo repositorio en GitHub
# Clónalo localmente
git clone https://github.com/tu-usuario/url-monitor.git
cd url-monitor

# Crea la estructura de carpetas
mkdir -p .github/workflows
```

### 2. Agregar los archivos

Copia los archivos proporcionados en esta estructura:

```
url-monitor/
├── .github/
│   └── workflows/
│       └── urlwatch.yml
├── urls.txt
├── urlwatch.yaml
└── README.md
```

### 3. Configurar URLs a monitorear

Edita `urls.txt` y agrega las páginas que quieres monitorear.

### 4. Push y activar

```bash
git add .
git commit -m "Initial setup"
git push
```

## 📧 Configurar Notificaciones (Opcional)

### Opción 1: Issues de GitHub (Más fácil)

Los cambios se verán en la pestaña "Actions" de tu repositorio.

### Opción 2: Telegram (Recomendado)

1. Crea un bot con @BotFather en Telegram
2. Obtén tu chat_id hablando con @userinfobot
3. Agrega secrets en GitHub:
   - Ve a Settings > Secrets > Actions
   - Agrega `TELEGRAM_BOT_TOKEN`
   - Agrega `TELEGRAM_CHAT_ID`
4. Descomenta la sección de Telegram en `urlwatch.yaml`

### Opción 3: Email

1. Crea una contraseña de aplicación en Gmail
2. Agrega `GMAIL_APP_PASSWORD` en GitHub Secrets
3. Descomenta la sección de email en `urlwatch.yaml`

## ⚙️ Personalización

### Cambiar frecuencia de chequeo

Edita el cron en `.github/workflows/urlwatch.yml`:

```yaml
- cron: '0 9 * * *'  # Diario a las 9 AM UTC
- cron: '0 */6 * * *'  # Cada 6 horas
- cron: '0 0 * * 1'  # Semanal (lunes)
```

### Ejecutar manualmente

Ve a Actions > URLWatch > Run workflow

## 📊 Ver resultados

- **Actions tab**: Logs de cada ejecución
- **Issues**: Si configuras notificaciones por issues
- **Telegram/Email**: Si configuras notificaciones

## 🎯 Ejemplos de filtros avanzados

```yaml
# Solo monitorear un selector CSS específico
name: "Precio del producto"
url: https://ejemplo.com/producto
filter:
  - css: .precio
  - strip
  
# Usar XPath
name: "Noticias destacadas"
url: https://noticias.com
filter:
  - xpath: //div[@class="destacado"]//h2
  
# Eliminar elementos no deseados
name: "Artículo sin ads"
url: https://blog.com/post
filter:
  - css: article
  - delete: .advertisement
  - delete: .comments
```

## 💡 Tips

- Usa filtros CSS para monitorear solo partes específicas
- GitHub Actions tiene 2000 minutos gratis/mes
- Los chequeos diarios usan ~1-2 minutos/día
- Puedes tener múltiples URLs en `urls.txt`

## 🔧 Troubleshooting

**No se ejecuta el workflow:**
- Ve a Actions y habilita workflows
- Verifica que el repositorio sea público

**No recibo notificaciones:**
- Revisa los logs en la pestaña Actions
- Verifica que los secrets estén configurados correctamente

**Demasiadas notificaciones:**
- Usa filtros CSS más específicos
- Aumenta el intervalo del cron