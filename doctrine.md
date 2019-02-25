# Doctrine

## Relations

### Define Relationships with Abstract Classes and Interfaces
```php
// src/Entity/Customer.php

namespace App\Entity;

use Acme\CustomerBundle\Entity\Customer as BaseCustomer;
use Acme\InvoiceBundle\Model\InvoiceSubjectInterface;

class Customer extends BaseCustomer implements InvoiceSubjectInterface
{
}
```

```php
// src/Acme/InvoiceBundle/Entity/Invoice.php

namespace Acme\InvoiceBundle\Entity;

use Acme\InvoiceBundle\Model\InvoiceSubjectInterface;
class Invoice
{
    /**
     * @ORM\ManyToOne(targetEntity="Acme\InvoiceBundle\Model\InvoiceSubjectInterface")
     * @var InvoiceSubjectInterface
     */
    protected $subject;
}
```

```php
// src/Acme/InvoiceBundle/Model/InvoiceSubjectInterface.php

namespace Acme\InvoiceBundle\Model;

interface InvoiceSubjectInterface
{
    /**
     * @return string
     */
    public function getName();
}
```

```yaml
# config/packages/doctrine.yaml
doctrine:
    # ...
    orm:
        # ...
        resolve_target_entities:
            Acme\InvoiceBundle\Model\InvoiceSubjectInterface: App\Entity\Customer
```