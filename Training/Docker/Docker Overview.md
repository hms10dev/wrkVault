 # 📝 Cornell Notes: Docker 

## Date: Aug 4, 2022

### Topic: Docker

---

## ❓ Questions/Cues
- Why do we need it?
	- 

## 📝  Notes
- Why Docker?
	- The Matrix of Hell
	- Compatibility Dependency
	- Different Dev/test/prod environments
	- otherwise Long setup time
- What can it do?
	Containerize apps,
	run each service in it's own [[Container]] with own dependencies

### Docker Commands:
| Command                        | Definition                                                                                            |     |
| ------------------------------ | ----------------------------------------------------------------------------------------------------- | --- |
| docker run <container name/>   | run the given service &  application                                                                  |     |
| docker ps                      | lists all running containers                                                                          |     |
| sleep 20                       | sleep for 20 seconds                                                                                |     |
| docker stop <containername/id> | stops container process                                                                               |     |
| docker rm  <contanername/id>   | removes container                                                                                     |     |
| docker rmi  <containername/id> | removes images[^1]                                                                                    |     |
| docker images                  | display the docker images                                                                             |     |
| docker pull                    | looks for local img, if can't find it then goes out and pullls img and runs container with that image |     |
| -d                             | runs in background                                                                                                      |     |
|                                |                                                                                                       |     |
|                                |                                                                                                       |     |

[^1]:Have to remove the containers before removing the image





When you don't specify a version number when you call a certain image/ container , the default tag, _latest_ is used.

By Default, A docker container does not listen to any standard input
just because it is accessed in the terminal, doesn't mean it will reach the input line

containers usually run in non-interactive modes

in order to provide input, you must map the standard input to the docker container using ==-i== parameter

inorder to view the container's term, use ==-t==

> -i = interactive mode
> -t = pseudoterminal



## 📑  Summary
Highlight ==what’s important!==