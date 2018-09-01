# \_\_I18N

```javascript
import React from "react";
import { i18n, createComponent } from "webiny-app";
const t = i18n.namespace("MyApp.ContactInformation");

class ContactInformation extends React.Component {
    render() {
        const phoneNumber = this.props.phoneNumber;
        const emailLink = <a href={`mailto:${this.props.email}`}>{this.props.email}</a>;
        
        return (
            <div>
                <div>{t`Contact information`}</div>
                <ul>
                    <li>{t`By phone: {phoneNumber}`({ phoneNumber })}</li>
                    <li>
                        {t`Or send an email to {emailLink}, we will respond as soon as possible.`({ emailLink })}
                    </li>
                </ul>
            </div>
        );
    }
}

export default createComponent(ContactInformation);
```

