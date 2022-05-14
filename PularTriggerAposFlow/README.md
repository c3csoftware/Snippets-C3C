# Pular trigger após um flow ser executado

Levando em consideração a ordem de execução do salesforce, é possível que você queria que os flows sejam executados sempre depois das triggers
Porém, temos um problema que não permite que isso seja executado com tanta precisão, pois quando se encerra um flow inicia-se a trigger novamente
e isso é bem ruim pois gera erro de lógica e um comportamento inesperado, levando em consideração esses pontos foi desenvolvido um bypass de trigger
que é acionado pelo flow.

---

## Passo a passo 
1. Primeiro é criado uma classe que pode ser chamada em flows. 

```java
public without sharing class ControlFlow 
{
  public static Boolean pularTrigger = false;

  @InvocableMethod
  public static void pularTrigger()
  {
    pularTrigger = true;
  }
}
```
> São criadas variáveis estáticos pois esses valores se mantém em contexto de execução, então é possível verificar o valor do variável pularTrigger quando uma trigger for acionada, pois a variável irá manter o estado.

> O método é criado com a annotation @InvocableMethod para que a mesma possa ser chamada no flow, com intuito de modificar o estado da variável pularTrigger.

2. Na trigger, basta realizar a verificação do estado da variável estática.

```Java
trigger MinhaTrigger on Lead (before insert, before update) 
{
  if (!ControlFlow.pularTrigger)
  {
    TriggerFactory();
  } else {
    system.debug('Pulou a execução da trigger, pois está vindo do flow');
  }
}
```

3. Chame o método criado no primeiro passo no início do seu flow, para que o estado da variável já altere de primeiro.
> Tente colocar essa ação antes de qualquer regra de negócio que seja necessário para a execução do flow, já para garantir que o valor da variável estática seja modificada.
