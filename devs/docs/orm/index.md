## ORM API

### Object Relational Mapping module:

* Hierarchical structure
* Constraints consistency and validation
* Object metadata depends on its status
* Optimised processing by complex query (multiple actions at once)
* Default field values
* Permissions optimisation
* Persistent object: DB postgresql
* Data conversion
* Multi-level caching system
* Two different inheritance mechanisms
* Rich set of field types:
* classical (varchar, integer, boolean, …)
* relational (one2many, many2one, many2many)
* functional

### Models
Model fields are defined as attributes on the model itself:

```python linenums="1"
from odoo import models, fields
class AModel(models.Model):
    _name = 'a.model.name'

    field1 = fields.Char()
```