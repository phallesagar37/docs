{% ifversion fpt or ghes > 3.1 or ghae or ghec %}
Além disso,
{% data variables.product.prodname_dotcom %} pode revisar todas as dependências adicionadas, atualizadas ou removidas em um pull request feita para o branch padrão de um repositório e sinalizar quaisquer alterações que introduziriam uma vulnerabilidade no seu projeto. Isso permite que você detecte e gerencie as dependências vulneráveis antes, e não depois, de elas alcançarem seu código. Para obter mais informações, consulte "[Revisar as mudanças de dependências em um pull request](/github/collaborating-with-issues-and-pull-requests/reviewing-dependency-changes-in-a-pull-request)".
{% endif %}
