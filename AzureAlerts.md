- [Azure Alerts](#azure-alerts)
  - [Alert rules](#alert-rules)
    - [Signal types](#signal-types)
  - [Action Groups](#action-groups)
    - [Notifications](#notifications)
    - [Actions](#actions)
  - [Tutorials](#tutorials)
 
# Azure Alerts

Benefits:

- Better notification system
- A unified authoring experience
- View Log Analytics alerts in Azure portal
- Separation of Fired Alerts and Alert Rules
- Better workflow.

You can alert on metrics and logs as described in monitoring data sources. These include but are not limited to:

- Metric values
- Log serarch queries
- Activity Log events
- Health of the underlying Azure platform
- Tests for web site availability

Details of alerts state [here](https://docs.microsoft.com/en-gb/learn/modules/configure-azure-alerts/2-manage-azure-monitor-alerts)

## Alert rules

Alerts proactively notify you when important conditions are found in your monitoring data. They allow you to identify and address issues before the users of your system notice them. Alerts consist of alert rules, action groups, and monitor conditions.

Alert rules are separated from alerts and the actions that are taken when an alert fires. The alert rule captures the target and criteria for alerting. The alert rule can be in an enabled or a disabled state. Alerts only fire when enabled. The key attributes of an alert rule are:

- **Target Resource** – Defines the scope and signals available for alerting. A target can be any Azure resource. Example targets: a virtual machine, a storage account, a virtual machine scale set, a Log Analytics workspace, or an Application Insights resource. For certain resources (like Virtual Machines), you can specify multiple resources as the target of the alert rule.
- **Signal** – Signals are emitted by the target resource and can be of several types. Metric, Activity log, Application Insights, and Log.
- **Criteria** – Criteria is a combination of Signal and Logic applied on a Target resource. Examples: * Percentage CPU > 70%; Server Response Time > 4 ms; and Result count of a log query > 100.
- **Alert Name** – A specific name for the alert rule configured by the user.
- **Alert Description** – A description for the alert rule configured by the user.
- **Severity** – The severity of the alert once the criteria specified in the alert rule is met. Severity can range from 0 to 4.
  - 0: Critical
  - 1: Error
  - 2: Warning
  - 3: Informational
  - 4: Verbose

- **Action** – A specific action taken when the alert is fired.

### Signal types

- **Metric** alerts provide an alert trigger when a specified threshold is exceeded. For example, a metric alert can notify you when CPU usage is greater than 95 percent.
- **Activity log** alerts notify you when Azure resources change state. For example, an activity log alert can notify you when a resource is deleted.
- **Log** alerts are based on things written to log files. For example, a log alert can notify you when a web server has returned a number of 404 or 500 responses.

## Action Groups

An action group is a collection of notification preferences defined by the owner of an Azure subscription. Azure Monitor and Service Health alerts use action groups to notify users that an alert has been triggered. Various alerts may use the same action group or different action groups depending on the user's requirements.

### Notifications

Notifications configure the method in which users will be notified when the action group triggers.

- **Email Azure Resource Manager role** - Send email to the members of the subscription's role. Email will only be sent to Azure AD user members of the role. Email will not be sent to Azure AD groups or service principals.
- **Email/SMS message/Push/Voice - Specify any email, SMS, push, or voice actions.

### Actions

Actions configure the method in which actions are performed when the action group triggers.

- **Automation runbook** - An automation runbook is the ability to define, build, orchestrate, manage, and report on workflows that support system and network operational processes. A runbook workflow can potentially interact with all types of infrastructure elements, such as applications, databases, and hardware.
- **Azure Function** – Azure functions is a serverless compute service that lets you run event-triggered code without having to explicitly provision or manage infrastructure.
- **ITSM** – Connect Azure and a supported IT Service Management (ITSM) product/service. This requires an ITSM Connection.
- **Logic App** – Logic apps connect your business-critical apps and services by automating your workflows.
- **Webhook** – A webhook is a HTTPS or HTTP endpoint that allows external applications to communicate with your system.

## Tutorials

[Use this link](https://docs.microsoft.com/en-gb/learn/modules/incident-response-with-alerting-on-azure/4-exercise-metric-alerts) to use an Azure lab to learn more on how to use metrica alerts.

