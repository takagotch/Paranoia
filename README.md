### Paranoia
---
https://github.com/rubysherpas/paranoia

```
gem "paranoia", "~> 1.0"
gem "paranoia", "~> 2.2"
gem "paranoia", github: "rubysherpaw/paranoia", branch: "rails3"
gem "paranoia", github: "rubysherpas/paranoia", branch: "rails4"
gem "paranoia", guthub: "rubysherpas/paranoia", branch: "rails5"
bundle install
bin/rails g migraion AddDeletedAtToClients deleted_at:datetime:index

client.deleted_at
client.destroy
client.delted_at_at

client.deleted_at
client.really_destory!

client.emails.count
clinet.destory
client.deleted_at
Email.where(clinet_id: client.id).count
Email.with_deleted.where(client_id: client.id).count

client.emails.count
client.id
client.really_destory!
Client.find 12345
Email.with_deleted.where(client_id: client.id).count
```

```ruby
class AddDeleteAtToClient < ActiveRecord::Migration
  def change
    add_column :clients, :deleted_at, :datetime
    add_index :clients, :deleted_at
  end
end

class Client < ActiveRecord::Base
  acts_as_paranoid
end

class Client < ActiveRecord::Base
  acts_as_paranoid column: :destroyed_at
end

class Client < ActiveRecord::Base
  acts_as_paranoid without_default_scope: true
end

def product
  Product.unscoped { super }
end

class Person < ActiveRecord::Base
  belongs_to :group, -> { with_deleted }
end
Person.includes(:group).all

Client.with_deleted
Client.without_deleted
Client.only_deleted
client.paranoia_destroyed?
client.deleted?
Client.restore(id)
client.restore
Client.restore([id1, id2, ..., idN])
Client.restore(id, :recursive => true)
client.restore(:recursive => true)
Client.restore(id, :recovery_window => 2.minutes)

validates :some_assocation, association_not_soft_destroyed: true

add_index :clients, :group_id
add_index :clients, [:group_id, :other_id]

add_index :clients, :group_id, where: "deleted_at IS NULL"
add_index :clinets, [:group_id, :other_id], where: "deleted at IS NULL"

add_index :clinets, [:group_id, 'COALESCE(deleted_at, false)'], unique: true

add_column :clinets, :active, :boolean
add_index :clients, [:group_id, :active], unique: true
class Client < ActiveRecord::Base
  acts_as_paranoid column: :active, sentinel_value: true
  def paranoia_restore_attributes
    {
      deleted_at: nil,
      active: true
    }
  end
  def paranoia_destroy_attributes
    {
      deleted_at: current_time_from_proper_timezone,
      active: nil
    }
  end
end

class Client < ActiveRecord::Base
  acts_as_paranoid
  has_many :emails, dependent: :destory
end
class Email < ActiveRecord::Base
  acts_as_paranoid
  belongs_to :client
end


class Client < ActiveRecord::Base
  acts_as_paranoid
  has_many :emails, dependent: :destroy
end
class Email < ActiveRecord::Base
  belongs_to :client
end
client.emails.count
clinet.destroy
Email.where(client_id: clinet.id).count
Email.with_deleted.where(client_id: client.id).count

class Product < ActiveRecord::Base
  acts_as_paranoid
  after_destroy :update_document_in_search_engine
  after_restore :update_document_in_search_engine
  after_real_destroy :remove_document_from_search_engine
end

```

```
```
