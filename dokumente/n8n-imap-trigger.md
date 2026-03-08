# n8n IMAP Trigger - Filter Regeln

["UNSEEN", ["FROM", "sensdesk@bellequip.at"]]

["UNSEEN", ["FROM", "SWPC.Products@noaa.gov"]]

Key Aspects of n8n Custom Email Rules

    Syntax: Rules must follow the node-imap format, typically using JSON-style arrays (e.g., ["UNSEEN", ["OR", ["SUBJECT", "Report"], ["TEXT", "Invoice"]]]).
    Common Filters: You can filter by UNSEEN (unread), FROM, SUBJECT, TEXT (body), or date.
    Implementation: Within the IMAP node, navigate to Options > Add Option > Custom Email Rules.
    Troubleshooting: If rules fail, try using double quotation marks and ensure the n8n version is updated.
    Alternative (AI): For advanced organization, you can use AI to classify and label emails, such as identifying urgent emails or specific topics. 

Common Custom Rule Examples

    Find Unread Invoices: ["UNSEEN", ["SUBJECT", "Invoice"]]
    Filter by Sender: ["FROM", "support@example.com"]
    Complex OR Logic: ["OR", ["SUBJECT", "Alert"], ["SUBJECT", "Error"]] 