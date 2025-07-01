# 🚀 Projeto DIO: Monitoramento de Máquinas Virtuais no Microsoft Azure

Este projeto faz parte do laboratório prático da DIO e tem como objetivo demonstrar como configurar o monitoramento eficaz de Máquinas Virtuais (VMs) no Microsoft Azure, utilizando recursos como Azure Monitor, Log Analytics, Activity Logs e regras de alerta. A documentação também serve como base de estudo para profissionais de Infraestrutura, Cloud e Segurança.

---

## 🎯 Objetivos do Projeto

- Aplicar os conceitos aprendidos no curso da DIO em um ambiente prático.
- Configurar e validar alertas para eventos críticos em VMs.
- Utilizar o Log Analytics e o Azure Monitor para análises e dashboards.
- Documentar todos os passos de forma clara, objetiva e reutilizável.
- Publicar a experiência em um repositório GitHub público como material de apoio técnico.

---

## 🛠️ Recursos Utilizados

- **Plataforma**: Microsoft Azure  
- **Serviços**:  
  - Azure Monitor  
  - Log Analytics  
  - Azure Alerts  
  - Activity Log  
- **Ferramentas de Apoio**:  
  - GitHub  
  - Markdown  
  - Kusto Query Language (KQL)

---

## 🧪 Etapas de Implementação

### 1. Criação da Máquina Virtual
- Criar uma nova VM no Azure (Windows Server ou Ubuntu).
- Configurar IP público, grupo de segurança e autenticação.
- Garantir que o diagnóstico esteja ativado durante a criação.

### 2. Criação do Log Analytics Workspace
- Ir para **Log Analytics Workspaces** no portal do Azure.
- Criar um novo workspace e associá-lo à VM.
- Verificar se a coleta de dados está ativa.

### 3. Habilitar Azure Monitor
- Acessar **Azure Monitor** > **Insights** > **Máquinas Virtuais**.
- Ativar a integração com a VM desejada.
- Visualizar métricas básicas: CPU, disco, rede, integridade.

### 4. Criar Regras de Alerta

#### a. Alerta de CPU Alta
- Tipo: Métrica
- Sinal: CPU Percentage
- Condição: Maior que 80% por 5 minutos
- Ação: Notificar via e-mail (grupo ou indivíduo)

#### b. Alerta de Exclusão de VM
- Tipo: Activity Log
- Operação: `Microsoft.Compute/virtualMachines/delete`
- Ação: Notificação + registro no Log Analytics

#### c. Alerta de Falha de Inicialização
- Métrica: Status de Inicialização
- Ação: Envio de alerta + webhook (para automação)

### 5. Consultas com Kusto Query Language (KQL)

#### Logs de Exclusão de VMs:
```kusto
AzureActivity
| where OperationNameValue == "Microsoft.Compute/virtualMachines/delete"
| project TimeGenerated, ResourceGroup, Caller, ActivityStatus
```

#### Eventos com Status “Failed”:
```kusto
AzureActivity
| where ActivityStatus == "Failed"
| project TimeGenerated, OperationName, ResourceGroup, Caller
```

#### Uso de CPU Acima de 80%:
```kusto
Perf
| where ObjectName == "Processor" and CounterName == "% Processor Time"
| where CounterValue > 80
| summarize avg(CounterValue) by bin(TimeGenerated, 5m), Computer
```

### 6. Criação de Dashboard com Workbooks
- Acessar “Workbooks” em Azure Monitor.
- Criar visualizações personalizadas: CPU, RAM, rede, alertas recentes.
- Salvar e compartilhar com a equipe de TI/Cloud.

---

## 📋 Boas Práticas de Monitoramento

- Habilite diagnósticos sempre que criar uma VM.
- Utilize **tags** para categorizar máquinas críticas.
- Crie grupos de ação reutilizáveis para alertas.
- Automatize respostas com **Logic Apps** ou **Azure Automation**.
- Use **Azure Policy** para prevenir exclusão de recursos essenciais.
- Armazene logs por pelo menos 30 dias para auditorias e investigações.

---

## 🧠 Lições Aprendidas

> "Monitorar não é apenas saber quando algo dá errado, mas também prever falhas antes que aconteçam."

Ao concluir esse projeto, ficou evidente a importância de **observabilidade em tempo real**, uso de **alertas proativos** e da **centralização de logs** como pilares de resiliência na nuvem. Além disso, o uso de KQL se mostrou extremamente poderoso para auditoria e análise técnica.

---

## 📚 Referências e Documentações Oficiais

- [✅ Introdução ao Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview)
- [📊 Monitoramento de Máquinas Virtuais](https://learn.microsoft.com/pt-br/azure/azure-monitor/vm/vminsights-overview)
- [📖 Guia de Consultas KQL](https://learn.microsoft.com/pt-br/azure/data-explorer/kusto/query/)
- [📘 GitHub Markdown Reference](https://guides.github.com/features/mastering-markdown/)
- [📓 Formação GitHub para Documentação Técnica](https://github.com/digitalinnovationone/github-certification)

---

## ✅ Status do Projeto

> 📌 **Projeto finalizado e entregue com sucesso.**  
> Este repositório está disponível para consulta pública e servirá como referência para futuros projetos na nuvem.
