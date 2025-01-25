# Ollama Docker Traefik Setup

This repository provides a Docker Compose setup for running Ollama with Traefik as a reverse proxy, making it accessible for Cursor AI integration.

## Getting Started

### Prerequisites
Make sure you have the following prerequisites installed on your machine:

- Docker with Docker Compose
- Traefik (configured as your reverse proxy)
- Cursor IDE

### Why you need Traefik for Cursor

Traefik is essential in this setup for several reasons:

1. **Secure Access**: Traefik provides HTTPS termination, ensuring that all communications between Cursor and your Ollama instance are encrypted.
2. **Domain Routing**: It allows you to expose Ollama through a custom domain, which is required for Cursor integration as the LLM should be accessible from the Cursor servers.
3. **Authentication**: Traefik can handle authentication layers, adding security to your LLM endpoint.
4. **Load Balancing**: If you scale your Ollama instances, Traefik can distribute the load effectively.

Without Traefik, you would need to manually configure SSL certificates and routing, which can be complex and error-prone.

### Configuration

1. Clone the Docker Compose repository:

    ```bash
    git clone https://github.com/pezzos/ollama-docker.git
    ```

2. Change to the project directory:

    ```bash
    cd ollama-docker
    ```

3. Configure your domain in the `.env` file:
    ```bash
    DOMAIN=your-domain.com
    ```

## Usage

Start Ollama and its dependencies using Docker Compose:

```bash
docker-compose up -d
```

Visit [https://chat.<DOMAIN>](https://chat.<DOMAIN>) in your browser to access Ollama-webui.

### Model Installation

Navigate to settings -> model and install a model (e.g., llava-phi3). This may take a couple of minutes, but afterward, you can use it just like ChatGPT.

## Use it in Cursor AI

### In OpenWeb UI
1. Create an API key:
   - Go to OpenWebui > settings > account > API key
   - Create a new key if you don't have one
   - Save this key securely

2. Add a model:
   - Install the model you want to use (ex: deepseek-coder:1.3b)
   - Wait for the installation to complete
   - Verify the model is working in the web UI

### Then in Cursor:

1. Open Cursor settings
2. In the AI models section:
   - Add the exact model name (case sensitive, ex: deepseek-coder:1.3b)
   - Disable other models to ensure you're using the right one
3. In the OpenAI configuration:
   - Paste your OpenWebUI API key
   - Add the API URL: https://chat.<DOMAIN>/api
4. Test the connection by trying a simple prompt

## Stop and Cleanup

To stop the containers and remove the network:

```bash
docker-compose down
```

To completely remove all data (including models):
```bash
docker-compose down -v
```

## Contributing

We welcome contributions! If you'd like to contribute to the Ollama Docker Traefik Setup:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

Please ensure your code follows our coding standards and includes appropriate documentation.

## License

This project is licensed under the [MIT License](LICENSE). Feel free to use, modify, and distribute it according to the terms of the license. We appreciate attribution and mentions in derivative works.

## Support

If you encounter any issues or have questions:
1. Check the existing issues on GitHub
2. Create a new issue with detailed information about your problem
3. Join our community discussions
