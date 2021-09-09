# C# KeyboardInterceptor

Windows low-level keyboard hook written in C#. This library was NOT created for malicious purposes.

## Installation
```PowerShell
Install-Package KeyboardInterceptor
```

## Usage
```csharp
var interceptor = new Interceptor(key =>{
	//Do something.
});

interceptor.Start(); //On application start.

interceptor.Stop(); //On application end.
```

### Custom Resolver
```csharp
public MyCustomResolver : IKeyResolver
{
	public void Resolve(Key key){
		//Do something.
	}
}
```

### Abstract Sequence Resolver
```csharp
public class ConcreteSequenceResolver : AbstractSequenceKeyResolver
{
    public ConcreteSequenceResolver(IEnumerable<Key> sequence) : base(sequence)
    {
    }

    protected override void OnSequenceEqual()
    {
        //Do something.
    }
}

var sequence = new[]{Key.A, Key.LControlKey, Key.D1};
var delayTolerance = 1000; // Min value = 400
var interceptor = new Interceptor(new ConcreteSequenceResolver(sequence){DelayTolerance = delayTolerance});
```
