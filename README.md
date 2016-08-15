thread.au3
==========

True multithreading for AutoIt3.

Note: this project is still under development and its use is really not recommended.

If you need something like threading, take a look on forking. See it [here](https://github.com/jesobreira/authread).

You're also welcome to fork this repo and help in developing!

Example
=======

Start by including the script.

```
#include 'thread.au3'
```

Call `CreateThread($sCallback)`. It will return the handle to the thread. As argument, specify the function you're going to create.

```
CreateThread("helloworld")
```

Create the specified function. Note that it must receive an argument (which is the handle to the thread, just like returned by CreateThread). If you forget the `$h` part (or any other name you choose for it), it will not work.

```
Func helloworld($h)
	MsgBox(0, "", "Hello from the sub thread")
EndFunc
```

Do anything you need in the main thread.

```
MsgBox(0, "", "Hello from the main thread")
```

And exit. Do not forget it.

```
Exit
```

We end up with this code:

```
#include 'thread.au3'

CreateThread("helloworld")

Func helloworld($h)
	MsgBox(0, "", "Hello from the sub thread")
EndFunc

MsgBox(0, "", "Hello from the main thread")

Exit
```

When you run it, you'll see two message boxes - which is not possible in singlethreading :)

Docs
====

So far just these two functions:

**hWnd CreateThread ( string $sCallback )**

Creates a new thread with the function name defined in $sCallback, and returns the handle to the new thread. Also, $sCallback will receive a handle to the own thread as the first and only function argument.

**boolean TerminateThread( hWnd $hWnd )**

Terminates a thread. $hWnd might come from CreateThread return or from the callback function argument. If you're calling TerminateThread from inside a thread, remember to Return it (`Return TerminateThread($h)`).