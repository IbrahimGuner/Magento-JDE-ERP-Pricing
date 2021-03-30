# Magento-ERP-Pricing

ERP (JDE) Pricing Needs to update Magento E-Commerce App
In order to achieve this goal 2 Main Updates Needs to be Done.

1) Magento Catalog Price Rule Needs to Updated to get the pricing info from the ERP System.
2) ERP Endpoint Needs to be created on the ERP side

Update 1)

Magento Catalog Price Rule Needs to Updated to get the pricing info from the ERP System.

Problem : Magento 2 Catalog Price Rule is not designed to get a pricing update from API End Points

Solution: Update Magento core with a new custom module 

Pricing update will be through an API Hookup

ERP Module Defined via WEBAPI interface will do the job, the module implementation details are below:

registration.php (extends catalogrule API)
module.xml (Module Name version 1.00, no Dependency)



Magento 2 Core Files Reference:-
app/code/Atrium/CatalogRule\Api\interface\CatalogRuleRepositoryInterface
app/code/Atrium/CatalogRule\Model\Rule.php

app/code/Atrium/CatalogRuleApi/etc/webapi.xml
webapi.xml for getting the list of all catalogRules 

Magento/CatalogRuleApi\Api\CatalogRuleRepositoryInterface
app/code/CatalogRuleApi/etc/di.xml
di.xml to specify the preference implementation classes for module and custom interface.


app/code/Atrium/CatalogRuleApi/Plugin/CatalogRuleRepositoryPlugin
Use Catalog Price Rules with GET List.

Execution REST API methods V1/catalogRules/:ruleId GET,POST



URL: rest/V1/catalogRules/:ruleId
Sample Request Format

{
“rule”: {
“name”: “pricing update”,
“description”: “JDE”,
“is_active”: 1,
“rule_condition”: {
“type”: “Magento\CatalogRule\Model\Rule\Condition\Combine”,
“attribute”: “”,
“operator”: “”,
“value”: “1”,
“is_value_parsed”: false,
“aggregator”: “all”,
“conditions”: [
{
“type”: “Magento\CatalogRule\Model\Rule\Condition\Product”,
“attribute”: “category_ids”,
“operator”: “()”,
“value”: “27”,
“is_value_parsed”: false,
“aggregator”: “”
}
]
},
“stop_rules_processing”: 1,
“sort_order”: 0,
“simple_action”: “none”,
“discount_amount”: 0,
“extension_attributes”: {
“website_ids”: [
“1”
],
“customer_group_ids”: [
“0”,
“2”
]
}
}
}




