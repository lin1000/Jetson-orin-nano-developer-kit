# Jetson-orin-nano-developer-kit
notes, links , and docs


# Notes about how to prepare and setup.

1. [Get Started With Jetson Nano Developer Kit](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit) include hardware layout
1. Second item
1. Third item
1. Fourth item 



# Notes about how to run Open Web UI and install ollama

1. Use Docker to run a Open Web UI instance 
```
#Use this one to run with default setting (no gpu and not depend on nvidia runtime)
sudo docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

#Use this one to run on gpu and nvidia runtime with predefined Ollama Base URL
sudo docker run -d -p 3000:8080 --gpus all --runtime=nvidia -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:cuda

note: --add-host=host.docker.internal:host-gateway 允許容器內的 Open WebUI 透過該網址直接連回主機的 Ollama 服務。
```

> you will be able to connect to http://localhost:3000/ via browser to ask question and chose model.



1. [Use Native Install to install Ollama model](https://www.jetson-ai-lab.com/tutorials/ollama/)
```
curl -fsSL https://ollama.com/install.sh | sh

note: It creates a service to run ollama serve on startup, so you can start using the ollama command right away.
```

2. run ollama command as a taste
```

lin1000@lin1000:~$ ollama 
                                                                                
  Welcome to Ollama!                                                            
                                                                                
  Run open models with your coding agents so you can spend less                 
  while keeping your data private.                                              
                                                                                
  Connect your apps                                                             
  Power your existing coding apps with open models                              
                                                                                
  Easily switch models                                                          
  Swap between frontier models in one click.                                    
                                                                                
  Your data stays yours                                                         
  Your prompt data is never logged or trained on.                               
                                                                                
  Press Enter to continue                              

  Create an account                                                             
                                                                                
  Create your account for access to faster, larger open models.                 
  Your data is never logged or trained on.                                      
                                                                                
    Sign up / sign in                                                           
  ▸ No thanks, I'll use Ollama locally                                      

```

3. [find the right model to fit into my memroy size (16GB)(https://ollama.com/library/qwen3.5:2b)

```
ollama run llama3.1:8b ==> WAS KILLED (NOT WORKING due to memory limitation)
ollama run qwen3.5:2b
```