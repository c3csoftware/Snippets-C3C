# ApexTest

Snippets para ajudar na hora de desenvolver classe de testes unitários

## Como instalar:

## Conteúdos:
## 1. Setup
> Snippet para criar o setupInjector com maior velocidade.
> Para utilizar basta executar o seguinte comando
```java
C3C_testeSetup
```
> Isso em classes apex.
> O seu retorno é:
```java
public static void setupInjector()
{
    // Para getInstance
    C3C_DIContainer_Injector.createInstance('NomeBinding', Test.createStub(INomeBinding.class, new NomeBindingStub()));

    // Para newInstance
    C3C_DIContainer_Injector.createInstance('NomeBinding', INomeBinding.class, 'NomeDaClasseDeTeste.NomeBindingStub');
}
```

## 2. Stub
> Snippet para criar as stubs mais rápida.
> Para utilizar, basta executar o seguinte comando.
```java
C3C_testeStub
```
> Isso em classes apex.
> O seu retorno é:
```java
public class Stub extends C3C_AbstractStub implements System.StubProvider
{
    public override Map<String, ClassTested> getMapClassTested()
    {
        return mapClassTested;
    }
    public override String getClassName()
    {
        return '';
    }

    public override Object methodCall(
        Object stubbedObject,
        String stubbedMethodName,
        Type returnType,
        List<System.Type> listOfParamTypes,
        List<String> listOfParamNames,
        List<Object> listOfArgs
    )
    {
        Object returnValue;

        switch on stubbedMethodName
        {
            when ''
            {
                  returnValue = null;
            }
        }

        return returnValue;
    }
}
```