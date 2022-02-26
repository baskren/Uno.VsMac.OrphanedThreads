# Uno.VsMac.OrphanedThreads
A demo project to illustrate the explosion of VsMac threads when editing a source code file in an Uno project

How to demonstrate this issue:

1. Open the solution in the repo using VsMac 2019 - or just create a new Uno Solution (without the WPF, UWP, GtK and Tizen projects).
2. Open the Main.xaml.cs file
3. Open the MacOS Activity Monitor and note the number of threads

<img width="996" alt="image" src="https://user-images.githubusercontent.com/2528888/155846056-934477f4-3454-429e-be81-cff64bad2929.png">

4. Manually type (do not paste) the following code (or just any reasonable code - it won't take long):

```
       void MethodA()
        {

        }

#if __IOS__
        void MethodB()
        {
        }
#elif __ANDROID__
        void MethodB()
        {

        }
#else
        void MethodB()
        {
        }
#endif
        void MethodC()
        {

        }

        void MethodD()
        {
            System.Diagnostics.Debug.WriteLine($"Pizza {21}");
        }

        void MethodE()
        {

        }

        void MethodF()
        {
            if (System.Console.CapsLock)
                System.Console.Write("caps");
        }

#if __IOS__
        void MethodG()
        {
        }
#endif
```

5. Note the significant increase in threads in MacOS Activity Monitor

<img width="996" alt="image" src="https://user-images.githubusercontent.com/2528888/155846201-62e7e8ec-8248-4ad4-ad32-9da4f293a98d.png">
