##########
Lesson One
##########

.. admonition:: A Note from the Author:

    I would like to state now, for the Record, that I am by no
    means qualified to write this.  I'm still baffled every single
    day by *something* in Python.  I often have **no idea** how to
    do whatever it is I'm trying to do.

    But I fucked around a whole bunch, and I *think* I maybe 'get it'
    enough to at least point you in the right direction.  And anyway,
    I've had fun writing (well, mostly *formatting*, all of this).

    Good luck!

*****
Setup
*****

Installation
============

If you're running Linux, you (probably) have Python installed by defualt.  For the purposes of this 'lesson', I'm going to just assume you're using something Debian-based (and thus use ``apt`` as your package manager).

You can check by opening a terminal and running the following command:

.. highlight:: python

.. code-block:: console
    
    which python

You should get the following output to the terminal:

.. code-block:: console
   :caption: Yours could be ../python or ../python3.x.x are acceptable as well

    /usr/bin/python3
    

(You may get some variant of this: /usr/bin/python, /usr/bin/python3.11.)

If you don't get a return, we'll need to go ahead and install Python:

.. code-block:: console
    
    sudo apt update && sudo apt full-upgrade -y
    sudo apt install python3


Note that your installation *may* be in a different location; as long as you get a return on the ``which`` command, you have Python installed.  Next, let's check which version of Python you're running; run the following in terminal:

.. code-block:: console
    
    python --version


If the above command fails (command not found), try:

.. code-block:: console
    
    python3 --version


If you get a return **now**, then you need to remember that in your configuration you need to run:

.. code-block:: console
    
    python3 [command]


as opposed to 

.. code-block:: console
    
    python [command]


(You can alias python3 to python by editing your .bashrc file; a quick Google should give you the info you need.)

Git
===

Now that we've got the Python interpreter installed and up to date, let's make sure we have a few git installed (more on this later):


.. code-block:: console
    
    sudo apt update && sudo apt full-upgrade -y
    sudo apt install git

That'll get git support running for you, but there's another package that I highly recommend: the GitHub CLI client.  While ``git`` will be fine for *most* of what we need to do with it, it doesn't really support credential management, which we're going to need to, for instance, download private repositories or push git packages to your GitHub account (without having to navigate to the website, login, yada yada).  Installing GitHub CLI can be a slight pain in the ass, so be very careful when copying the following commands:


.. code-block:: console
    
    type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
    curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
    sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
    sudo apt update 
    sudo apt install gh -y


Like I said, it's a lot of finicky, esoteric CLI stuff.  However, you shouldn't have too much trouble -- and it's not the absolute end of the world if you can't get ``gh`` installed (though, again, it'd be super nice to have).

Assuming you *did* get it installed, we'll go ahead and setup your account so we don't have to fuck with it later.  Run the following command and then follow the on-screen prompt(s):


.. code-block:: console
    
    gh auth login


.. note::
    
    When asked, I'd suggest logging in via web browser as opposed to an auth key, just because the latter is kind of a huge pain in the ass in my experience; YMMV.

That should be about all we need right now to at least get started running some Python code.  We'll install our IDE [Integrated Development Environment, *probably*] here in a minute.


*******
Python3
*******

Interactive
===========

So Python can be run in a couple of different ways.  The way you're probably already (at least marginally) aware of is as a script, or a package, or an application -- really all the same thing, just with different sizes and layers of complexity.

For the moment, though, let's loook at the *other* way we can run Python: in an interactive environment!

When we run Python interactively, we evaluate our commands in real time (as opposed to running a program, where everything happens step by step as written.)

Go ahead and open a terminal and run:

.. code-block:: console
    
    python3


You should get some lines of info that look something like this:

.. code-block:: console
    
    python3
    Python 3.11.2 (main, Mar 13 2023, 12:18:29) [GCC 12.2.0] on linux
    Type 'help', 'copyright', 'credits' or 'license' for more information.
    >>>


Notice that your prompt has changed to >>>.  This means you're now running the Python interactive interpreter.  It can take commands just like your regular terminal -- although the commands are entirely different, since Python has its own syntax, of course.

Let's try a couple commands now::

    >>> print("Hello world")

.. admonition:: Syntax Highlighting
    
    From here on out, if it's Python code (as opposed to bash/terminal commands), it'll be colorized syntactically to make it easier to see what's going on, as well as to disambiguate it from bash code.

If everything's working correctly, it should print "Hello world" to the console::

    >>> print("Hello world")
    Hello world

There -- your first Python command!  Congratulations, I guess!

Baby's First Method
===================

So, obviously, printing a message to the console is literally the least interesting thing we could do in Python.  Let's get just a tiny bit more interesting:

.. code-block::    
    :linenos:
    
    >>> message="Hello world"
    >>> print(message)
    Hello world

So what did we do here?  Well, ``message="Hello world"`` is an example of *assigning a variable*.

On line 1 we create (*instantiate*) the variable (``message``) and assign it (``=``) the *value* ``"Hello world"``.

On line 2 we tell Python to use the ``print()`` *method* to display the *value* of our *variable*, ``message`` -- in this instance, ``message`` is the *argument* we're *passing to* the ``print()`` *method*.


Vocab
=====

argument
    The 'thing' which is being acted upon by a **method** or **function** call;
    in this case -- but not *necessarily* -- it's our **variable**, ``message``.

function
    A collection of various **methods** ran in sequence.

instantiate
    To create an 'object'.

method
    A way of doing a thing.  ``print()`` is a **method**; when we 'use'
    a **method**, we say we *called* the **method**

parameter
    The generic name for what a **function** or **method** call *takes* as its'
    argument.  In the case of ``print()``, it has no defined **parameters**:
    you can enter *any* **value** inside the parenthesis and it'll (mostly)
    work.

value
    The actual *content* of a **variable**; what that **variable** is 'worth' --
    in this example, our **variable**'s **value** is ``"Hello world"``.

variable
    An object that can store **value**.  In our case, ``message`` is the
    variable, but we could just as easily have called our variable ``Frank``,
    and it'd still have worked as intended.

.. admonition:: Overwhelmed Yet?

    We're going to get back to setting up your PC now so we can call Lesson One "finished",
    but I just wanted you to have seen and heard some of this stuff before we move on.  Plus,
    I wanted you to check out the interactive shell -- we won't be using it much going
    forward.

******
VSCode
******

Installation
============

Okay, I'm going to *try* to make this as straightforward as possible -- hopefully nothing gets too fucky, but I've had some problems in the past installing VSCode on certain distros.  Debian-based distros (like Ubuntu) *tend* to work alright, but who knows?  

So, first things first, go to the website and download the .deb from `VSCode <https://code.visualstudio.com/download>`_.

Once you've got the .deb downloaded, open a terminal and navigate to whatever directory the .deb is located in (probably ~/downloads, but YMMV).

When you're in the directory, go ahead and run:

.. code-block:: console
    
    sudo apt install ./<filename>.deb

.. note::
    
    There's a (small) chance the above command fails; this is probably due to an issue with apt.  If it does, you might need to run ``sudo dpkg -i <filename.deb>`` to depackage the files and then ``sudo apt-get install -f`` to download the dependencies.  Probably won't come to that, though.

After you've completed the dependency install (using either of the two above methods), there's one more package we need to pick up, and then we can install VSCode.  Run the following:

.. code-block:: console
    
    sudo apt install apt-transport-https
    sudo apt update && sudo apt upgrade -y
    sudo apt install code

At this point, you should have VSCode installed correctly.  You can check it by either opening it through your file manager (like the Windows Start menu sort of thing) or, my preferred method, you can open it via terminal with the command ``code``.

.. caution::
    
    If you open it via terminal, running the command ``code`` will open VSCode to its default Welcome screen.  This is fine, but sometimes (usually), you might find it easier to run it with ``code .``.  This will open *any editable files in the current directory* in VSCode, so be cognizant of what directory you're in when you run it that way or you might be in for a helluva long load time.

So, assuming you have VSCode up and running correctly, we should now be more-or-less ready to start actually learning to code -- onward!