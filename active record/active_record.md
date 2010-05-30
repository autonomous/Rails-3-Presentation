!SLIDE
# Active Record #
***



!SLIDE
# ... and ARel #

***

!SLIDE code smaller
    @@@ruby
    # Article.find(:all, :order => "published_at desc", :limit => 10)
    Article.order("published_at desc").limit(10)

***

    @@@ruby
    # Article.find(:all, 
    #   :conditions => ["published_at <= ?", Time.now], 
    #   :include => :comments)
    Article.where("published_at <= ?", Time.now).includes(:comments)

***

    @@@ruby
    # Article.find(:first, :order => "published_at desc")
    Article.order("published_at").last

!SLIDE

# Lazy loading #

!SLIDE commandline incremental

    $ articles = Article.order("name")
    #<ActiveRecord::Relation:0x00000101669b90 @table=#<Arel::Table:0x000001023e9af8 
    @name="articles", @options={:engine=>#<Arel::Sql::Engine:0x000001023a15c8 @ar=ActiveRecord::Base,
    @adapter_name="SQLite">}, @engine=#<Arel::Sql::Engine:0x000001023a15c8 @ar=ActiveRecord::Base,
    @adapter_name="SQLite">, …

    $ articles.first
    => #<Article id: 2, name: "Can't See Me", published_at: nil, hidden: false, 
    created_at: "2010-02-22 20:37:03", updated_at: "2010-02-22 20:37:03">
    
!SLIDE bullets incremental

# This is cool because... #
    
* Simplifies this like caching
* Query construction   
* Suggestions?

!SLIDE code smaller

    @@@ruby
    # Inside your controller
    def index
      @items = Item.limit(10).order('created_at DESC')

      if logged_in?
        @items = @items.where('user_id = ', current_user) 
      end

      @items = @items.where('active = ?', !historical?) 
    end
***
    @@@ruby
    # Inside your view
    cache('items') do
      @items.each do |item|
        ...
      end
    end


!SLIDE

# What about named_scope? #

!SLIDE code smaller

    @@@ruby
    # named_scope :visible, :conditions => ["hidden != ?", true]  
    scope :visible, where("hidden != ?", true)

*** 
   
    @@@ruby
    # named_scope( :published, 
    #   lambda { 
    #     {:conditions => ["published_at <= ?", Time.zone.now] }
    #   }
    # )
    scope( :published, 
      lambda { where("published_at <= ?", Time.zone.now) }
    )

***
   
    @@@ruby
    # Easily chain scopes together
    scope :recent, visible.published.order("published_at desc")
    
!SLIDE code small
# New finder methods #
    @@@ruby
    where( :conditions )
    having( :conditions )
    select
    group
    order
    limit
    offset
    joins
    includes(:include)
    lock
    readonly
    from

!SLIDE code small
# CRUD #
    @@@ruby
    new( attributes )
    create( attributes )
    create!( attributes )
    find( id_or_array )
    destroy( id_or_array )
    destroy_all
    delete( id_or_array )
    delete_all
    update( ids, updates )
    update_all( updates )
    exists?