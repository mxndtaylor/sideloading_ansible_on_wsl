# sideloading ansible on wsl
I am attempting to achieve a set up that will allow me to simulate the management of one or more servers with ansible, all on wsl

## why on earth am I doing this?
I wanted to learn ansible, and since I'm not made of money, I don't have access to servers to play around with.  
Then when I was trying to use JetBrains CLion IDE with Alpine or Ubuntu, I was running into all sorts of environment configuration overhead.

So, then I thought that using ansible might be a way I could easily set a WSL instance up to deal with this.  
I searched around looking for a way of doing this, but most results involving wsl and ansible together involved instructions on how to install it there.  
Maybe I was looking in the wrong places, or didn't know what to search, but I really couldn't find it.

As a caveat, it may be possible to simply host containers within an existing linux distro and then connect ansible to them.  
But this breaks the container best practice of not modifying the container during runtime, and seems like more trouble than it's worth.  
Like at that point, why not just use a container image alone? And I want to learn ansible.

## why sideload a custom wsl distro?

One of the things I realized is that I wanted these instances to be "per-project" right?  
Because at this point I'm aiming for something like a Docker's Dev Environments or a python venv, but:  
* a less closed system than docker's solution
* a more generic and extensible solution than python venv 

If I wanted that, then every time I booted up the project it would overwrite the entirety of the existing wsl instance.  
That means I should want a separate instance for each project, or at least a couple instances so I can use them with multiple projects at the same time.  

## process start

I'm starting with an article from Microsoft about building custom distros here:  
https://learn.microsoft.com/en-us/windows/wsl/build-custom-distro

As recommended in the article, I'll be working from their repo:  
https://github.com/Microsoft/WSL-DistroLauncher (latest commit [32f88e8](https://github.com/microsoft/WSL-DistroLauncher/commit/32f88e8426d31dc6bf06c6711ec7a85edefe554f) as of writing this)

I don't know C/C++ _very_ well, but they're not unknown to me and I'm more than happy to learn.  
I'll also see about using Rust if possible since I enjoy it, but more than likely it will introduce too much complexity.
