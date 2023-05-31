# Publishing books

<v-clicks>

It will configure this route for your `apply_state_machine_transition` operation.

```php {all|17|17,3}
namespace App\Entity;

use Sylius\Component\Resource\Metadata\ApplyStateMachineTransition;
use Sylius\Component\Resource\Metadata\BulkDelete;
use Sylius\Component\Resource\Metadata\Index;
use Sylius\Component\Resource\Metadata\Create;
use Sylius\Component\Resource\Metadata\Delete;
use Sylius\Component\Resource\Metadata\Resource;
use Sylius\Component\Resource\Metadata\Update;
use Sylius\Component\Resource\Model\ResourceInterface;

#[Resource]
#[Create]
#[Update]
#[BulkDelete]
#[Delete]
#[ApplyStateMachineTransition(stateMachineTransition: 'publish')]
#[Index]
class Book implements ResourceInterface
{
}

```

</v-clicks>

---

# Route

<v-clicks>

It will configure this route for your `apply_state_machine_transition` operation.

| Name              | Method     | Path                |
|-------------------|------------|---------------------|
| app_book_publish  | PUT, PATCH | /books/{id}/publish |      


</v-clicks>

---

```php {all|14-19|15|16|17}
final class BookGrid extends AbstractGrid implements ResourceAwareGridInterface
{
    // [...]

    public function buildGrid(GridBuilderInterface $gridBuilder): void
    {
        $gridBuilder
            // [...]
            ->addField(
                StringField::create('author')
                    ->setLabel('sylius.ui.author')
                    ->setSortable(true)
            )
            ->addField(
                TwigField::create('state', '@SyliusUi/Grid/Field/state.html.twig')
                    ->setLabel('sylius.ui.state')
                    ->setOption('vars', ['labels' => 'admin/book/label/state']),
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

```twig
<!-- templates/admin/book/label/draft.html.twig -->
<span class="ui blue label">
    <i class="inbox icon"></i>
    {{ value|trans }}
</span>

```


---
layout: image
image: /publishing_book_01.png
transition: fade
---

---

```php {all|12-24|12|13|14|15-24|16-21|22|23}
final class BookGrid extends AbstractGrid implements ResourceAwareGridInterface
{
    // [...]

    public function buildGrid(GridBuilderInterface $gridBuilder): void
    {
        $gridBuilder
            // [...]
            ->addActionGroup(
                ItemActionGroup::create(
                    UpdateAction::create(),
                    Action::create('publish', 'apply_transition')
                        ->setLabel('app.ui.publish')
                        ->setIcon('icon: checkmark')
                        ->setOptions([
                            'link' => [
                                'route' => 'app_admin_book_publish',
                                'parameters' => [
                                    'id' => 'resource.id',
                                ],
                            ],
                            'class' => 'green',
                            'transition' => 'publish',
                        ]),
                    DeleteAction::create(),
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
image: /publishing_book_02.png
transition: fade
---

---
layout: image
image: /publishing_book_03.png
transition: fade
---
