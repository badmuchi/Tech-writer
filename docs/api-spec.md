# Interactive API Reference

Below is the interactive Swagger UI generated directly from our OpenAPI specification. You can explore the endpoints and response structures in real-time.

<link rel="stylesheet" href="https://unpkg.com/swagger-ui-dist@5/swagger-ui.css">
<script src="https://unpkg.com/swagger-ui-dist@5/swagger-ui-bundle.js"></script>

<div id="swagger-ui"></div>

<script>
  window.onload = function() {
    const ui = SwaggerUIBundle({
      url: '../openapi.yaml',
      dom_id: '#swagger-ui',
      deepLinking: true,
      presets: [
        SwaggerUIBundle.presets.apis,
        SwaggerUIBundle. somePresets || SwaggerUIBundle.presets.requestedService
      ]
    });
  };
</script>