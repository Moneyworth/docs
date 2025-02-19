1. Crea un token de acceso personal nuevo (PAT) con los alcances adecuados para las tareas que quieres realizar. Si tu organización requiere SSO, debes hablitarlo para tu token nuevo.
  {% warning %}

  **Nota:** Predeterminadamente, cuando seleccionas el alcance `write:packages` para tu token de acceso personal (PAT) en la interface de usuario, también se seleccionará el alcance `repo`. El alcance `repo` ofrece un acceso amplio e innecesario, el cual te recomendamos no utilices para los flujos de trabajo de GitHub Actions en particualr. Para obtener más información, consulta la sección "[Fortalecimiento de la seguridad para las GitHub Actions](/actions/getting-started-with-github-actions/security-hardening-for-github-actions#considering-cross-repository-access)". As a workaround, you can select just the `write:packages` scope for your PAT in the user interface with this url: `https://{% ifversion fpt or ghec %}github.com{% else %}HOSTNAME{% endif %}/settings/tokens/new?scopes=write:packages`.

  {% endwarning %}

    - Selecciona el alcance `read:packages` para descargar imágenes de contenedor y leer sus metadatos.
    - Selecciona el alcance `write:packages` para descargar y cargar imágenes de contenedor y leer y escribir sus metadatos.
    - Selecciona el alcance `delete:packages` para borrar las imágenes de contenedor.

  Para obtener más información, consulta la sección "[Crear un token de acceso personal para la línea de comandos](/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)".

2. Guarda tu PAT. Te recomendamos guardar tu PAT como una variable de ambiente.
  ```shell
  $ export CR_PAT=YOUR_TOKEN
  ```
3. Utilizando el CLI para tu tipo de contenedor, ingresa en el
{% data variables.product.prodname_container_registry %} service at `{% data reusables.package_registry.container-registry-hostname %}`.
  {% raw %}
  ```shell
  $ echo $CR_PAT | docker login {% endraw %}{% data reusables.package_registry.container-registry-hostname %}{% raw %} -u USERNAME --password-stdin
  > Login Succeeded
  ```
  {% endraw %}
