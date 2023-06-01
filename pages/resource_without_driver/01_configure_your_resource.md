```php{all|7|7,3|8|10|10,4|10,4,19-22}
namespace App\BoardGameBlog\Infrastructure\Sylius\Resource;

use Sylius\Component\Resource\Metadata\Resource;
use Sylius\Component\Resource\Model\ResourceInterface;
use Symfony\Component\Validator\Constraints\NotBlank;

#[Resource(
    alias: 'app.board_game',
)]
final class BoardGameResource implements ResourceInterface
{
    public function __construct(
        public ?string $id = null,
        #[NotBlank] public ?string $name = null,
        public ?string $shortDescription = null,
    ) {
    }

    public function getId(): string
    {
        return $this->id;
    }
}

```
