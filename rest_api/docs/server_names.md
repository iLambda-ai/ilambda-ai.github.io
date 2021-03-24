# Servers in EDA Cloud

## CCU
Every customer will have a group of isolated server components in EDA Cloud to maximize data security and service stability. We call it Customer Cloud Unit, CCU for short.

EDA assigns each CCU a domain name so that customers can access to the API easily. 

For example in North American, a customer with customer ID "foo" will be assigned domain name "foo.cloud.ilambda.com".

The rule to figure out CCU domain is:

```<customerID>.cloud.ilambda.com```

## CCU components

All the API provided in EDA are hosted by server components in a specific CCU. Domain names are also assigned for easier access. 

All the API must be accessed through **https** instead of http.

### Data Collector

Data collector is a component responsible for all data upload.

The nameing rule is as following:

```data-collector.<customerID>.cloud.ilambda.com```

### EDA Online Serving
EDA Online Serving is a core component to provide online recommendation service capability. It is designed to be high performance and high available, to be a rock solid part of mission critical environment.

The nameing rule is as following:

```eda.<customerID>.cloud.ilambda.com```
