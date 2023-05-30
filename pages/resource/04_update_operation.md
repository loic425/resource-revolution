# Editing books

<v-clicks>

`Update` operation allows to edit an existing item of your resource.

```php {all|11|11,6}
namespace App\Entity;

use Sylius\Component\Resource\Metadata\Index;
use Sylius\Component\Resource\Metadata\Create;
use Sylius\Component\Resource\Metadata\Resource;
use Sylius\Component\Resource\Metadata\Update;
use Sylius\Component\Resource\Model\ResourceInterface;

#[Resource]
#[Create]
#[Update]
#[Index]
class Book implements ResourceInterface
{
}

```

</v-clicks>

---

# Route

<v-clicks>

It will configure this route for your `update` operation.

| Name            | Method          | Path             |
|-----------------|-----------------|------------------|
| app_book_update | GET, PUT, PATCH | /books/{id}/edit |


</v-clicks>

---

```php {all|19-23|19|20|21}
final class BookGrid extends AbstractGrid implements ResourceAwareGridInterface
{
    // [...]

    public function buildGrid(GridBuilderInterface $gridBuilder): void
    {
        $gridBuilder
            ->orderBy('name', 'asc')
            ->addField(
                StringField::create('name')
                    ->setLabel('sylius.ui.name')
                    ->setSortable(true)
            )
            ->addField(
                StringField::create('author')
                    ->setLabel('sylius.ui.author')
                    ->setSortable(true)
            )
            ->addActionGroup(
                MainActionGroup::create(
                    CreateAction::create(),
                )
            )
        ;
    }

    public function getResourceClass(): string
    {
        return Book::class;
    }
}

```

---
layout: image
image: /adding_book_01.png
transition: fade
---

---
layout: image
image: /adding_book_02.png
transition: fade
---

---
layout: image
image: /adding_book_03.png
transition: fade
---

---
layout: image
image: /adding_book_04.png
transition: fade
---

---
layout: image
image: /adding_book_05.png
transition: fade
---
