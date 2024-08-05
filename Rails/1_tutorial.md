# Tổng quát

- Ruby là một ngôn ngữ lập trình hướng đối tượng, được biên dịch trong quá trình chạy.
  - Ruby là ngôn ngữ thông dịch, được biên dịch trong quá trình chạy. Mã nguồn Ruby được biên dịch thành mã máy hoặc bytecode sau đó được thực thi bởi máy ảo Ruby hoặc bộ thông dịch.
  - C++, Java là ngôn ngữ biên dịch. Mã nguồn được biên dịch trước thành mã máy hoặc bytecode trước khi chạy.
- Ruby được lấy cảm hứng từ các ngôn ngữ lập trình khác như Perl, Smalltalk, Effiel và Lisp.
- Trong Ruby, mọi thứ đều là đối tượng. Tất cả thông tin và mã đều có thể gán thông tin (thể hiện qua biến) và hành động (thể hiện qua hàm)

- Rails framework được tạo ra để quá trình phát triển phần mềm diễn ra nhanh hơn
- Rails sử dụng các quy ước triệt để và đảm nhận xử lý rất nhiều task khiến người lập trình viên không phải bận tâm về nó nữa như : mail management, object-database mappers, file structures, code generation .v.v.
- Rails sử dụng mẫu kiến trúc Model - View - Controller (MVC) để tăng cường khả năng bảo trì và phát triển của úng dụng.

[LINK](https://viblo.asia/p/series-huong-dan-lap-trinh-ruby-on-rails-phan-8-cac-ky-thuat-trong-rails-ban-nen-biet-WAyK8RWnlxX)

# Mô hình MVC trong Rails Framework

- [ActiveRecord](#active_record) đóng vai trò là M trong MVC:
  - Đóng vai trò xử lý các nghiệp vụ và logic, kết nối Database.
  - Tất cả các Model được tạo ra từ lệnh `rails g model <model name>` đều được kết thừa từ lớp ActiveRecord.
  - Đảm bảo Rails có thể hoạt động một cách độc lập với các hệ quản trị CSDL.

- [ActionView](#action_view) đóng vai trò là V trong MVC:
  - View trong Rails được viết bằng cách nhúng các đoạn mã Ruby trong các thẻ lẫn với thẻ HTML.
  - Rails hỗ trợ các `ActionView::Helper` để lập trình viên có thể dễ dàng hiển thị dữ liệu từ Model đến người dùng.
  - Một số Helper hỗ trợ trong việc tạo form dữ liệu : [FormTagHelper](https://apidock.com/rails/ActionView/Helpers/FormTagHelper)

- [ActionController](#action_controller) đóng vai trò là C trong MVC:
  - Trong Rails chỉ có application_controller.rb mới kế thừa từ lớp ActionController, tất cả các Controller khác đều kế thừa lại từ application_controller.rb. 
  - Controller có nghiệm vụ xác định các request và trả về view cho người dùng.

![rails_mvc](/imgs/rails_mvc.webp)

# Ruby on Rails Basic Technical

## <a name="active_record"></a> ActiveRecord - Model

Model << ActiveRecord (sử dụng cơ chế ORM(Object Relational Mapping) để tương tác với Database)

### [Query Interface](http://guides.rubyonrails.org/active_record_querying.html#conditions)

- Ứng dụng Rails sử dụng ActiveRecord để tương tác với database
- Việc sử dụng ActiveRecord giúp Rails độc lập với Database, việc query dữ liệu không sử dụng cú pháp của database.
- Các câu lệnh SQL được thay thế bằng Query Interface

- Các kĩ thuật nâng cao:
  - Lazy loading & Eager loading: cơ chế load các đối tượng của rails khi truy vấn
  - [Includes & joins](#includes_joins): loại bỏ N+1 query, tối ưu truy vấn
  - Scope : tránh việc lặp lại các truy vấn query được sử dụng ở nhiều nơi. 
  - Find or build object: find_or_create_by (tìm và khởi tạo - lưu vào CSDL), find_or_initialize_by (tìm và khởi tạo - không lưu vào CSDL)
  - find_by_sql: 

`Client.find_by_sql("SELECT * FROM clients INNER JOIN orders ON clients.id = orders.client_id ORDER BY clients.created_at desc")`

### [Associations](http://guides.rubyonrails.org/association_basics.html)

- Association là sự kết nối giữa 2 ActiveRecord models, nó sẽ tạo ra các hành động chưng đơn giản dễ dàng cho việc truy vấn CSDL.
- Các kiểu Associations:
  - belongs_to
  - has_one
  - has_many
  - has_many :through
  - has_one :through
  - has_and_belongs_to_many

### [Validations](http://guides.rubyonrails.org/active_record_validations.html)

- Đảm bảo rằng chỉ những dữ liệu hợp lệ mới được lưu vào DB. Giúp ta khởi tạo các điều kiện ràng buộc cho dữ liệu sẽ được lưu trữ
- Các validations helper thường dùng:
  -  presence: yêu cầu attributes không được empty (nil hoặc "", " ")
  -  length: yêu cầu độ dài giá trị của attributes. (maximum, minimum)
  -  uniqueness: yêu cầu giá trị của attributes phải là duy nhất
  -  format: yêu cầu giá trị của attributes phải match với một biểu thức chính quy Regular Expression

### [Callbacks](http://guides.rubyonrails.org/active_record_callbacks.html)

- Vòng đời của đối tượng (The Object Life Cycle) sẽ trải qua các giai đoạn created, updated, destroyed.
- ActiveRecord cung cấp các phương thức để móc vào vòng đời của đối tượng để thực hiện các hành động chúng ta mong muốn, các phương thức ấy gọi là Callback.
- Callbacks là những method được gọi vào các giai đoạn nhất định trong object's life cycle.

- Các callbacks được cung cấp sắn bởi Active Record:
  - Creating an Object
    ```    
    before_validation
    after_validation
    before_save
    around_save
    before_create
    around_create
    after_create
    after_save
    after_commit / after_rollback
    ```
  - Updating an Object
    ```
    before_validation
    after_validation
    before_save
    around_save
    before_update
    around_update
    after_update
    after_save
    after_commit / after_rollback
    ```
  - Destroying an Object
    ```    
    before_destroy
    around_destroy
    after_destroy
    after_commit / after_rollback
    ```
  - after_initialize and after_find
  - after_touch

### [Migration](http://guides.rubyonrails.org/active_record_migrations.html)

- Migrations là một đặc trưng của ActiveRecord cho phép bạn chỉnh sửa cấu trúc của Database theo thời gian.

### [Nested attributes](http://api.rubyonrails.org/classes/ActiveRecord/NestedAttributes/ClassMethods.html)

- Cho phép các đối tượng con có thể được tạo, cập nhật đồng thời với đối tượng cha

#### <a name="includes_joins"></a> Includes vs Joins

https://viblo.asia/p/includes-vs-joins-in-rails-when-and-where-gDVK2aDr5Lj


## <a name="action_view"></a> ActionView - View

### [ERB Template](http://guides.rubyonrails.org/action_view_overview.html#templates)

- Embedded Ruby (ERB) là một tính năng cho phép bạn nhúng code Ruby vào một trang HTML.

### [Partial](http://guides.rubyonrails.org/action_view_overview.html#partials)

- Tách source code ở view ra thành các file riêng biệt nhằm mục đích tái sử dụng.
`<%= render "shared/menu" %>`

### [FormHelper](http://guides.rubyonrails.org/action_view_overview.html#formhelper)

- Là các thẻ HTML được customize lại theo sourcce code của Ruby, giúp người đùng dễ dàng tương tác với view và model.

```
<%= form_for @person, url: { action: "update" } do |person_form| %>
  First name: <%= person_form.text_field :first_name %>
  Last name : <%= person_form.text_field :last_name %>

  <%= fields_for @person.permission do |permission_fields| %>
    Admin?  : <%= permission_fields.check_box :admin %>
  <% end %>
<% end %>
```

### [CacheHelper](http://guides.rubyonrails.org/action_view_overview.html#cachehelper)

- Rails sử dụng cơ chế template để load tất cả các view vào một file layout. Việc load này bao gồm tất cả các file js, cs.
- content_for: cho phép render các file chính vào layout chính, từ các view khác

## <a name="action_controller"></a> ActionController - Controller

### [Strong Parameters](http://guides.rubyonrails.org/action_controller_overview.html#strong-parameters)

- Cho phép cập nhật các attributes cụ thể trong Model.
- Ngăn chặn người dùng truyền vào các thuộc tính không mong muốn.

### [Filter](http://guides.rubyonrails.org/action_controller_overview.html#filters)

- Là methods được chạy `before`, `after`, `around` trong controller action

### [Render XML and JSON data](http://guides.rubyonrails.org/action_controller_overview.html#rendering-xml-and-json-data)

- Render data về định dạng XML hoặc JSON

### [Routing](http://guides.rubyonrails.org/routing.html#resource-routing-the-rails-default)

- resources: sinh ra 7 routes cho 7 method tương ứng theo Restful
  ```
  index
  new
  create
  show
  edit
  update
  destroy
  ``` 
- resource: sinh ra 6 routes cho 6 method
  ```
  new
  create
  show
  edit
  update
  destroy
  ```

### [Path and URL Helpers](http://guides.rubyonrails.org/routing.html#path-and-url-helpers)

- Thay thế việc sử dụng string fix route bằng các helper tương ứng
`photos_path returns /photos`

# Gem Support

- Các gem hỗ trợ cho việc phát triển ứng dụng Rails.
- Rails là 1 framework được xây dựng trên ngôn ngữ Ruby bao gồm một số gem được tích hợp sẵn.

## Gem hỗ trợ authentication

- Devise
- Clearance

## Gem hỗ trợ phân quyền user

- Cancancan
- role_authorization

## Gem hỗ trợ mã hóa password

- bcrypt
- scrypt

## Gem hỗ trợ phân trang

- page (recomment)
- kaminary
- will_paginate

## Gem hỗ trợ tìm kiếm

- ransack: search theo các fields trong ActiveRecord
- searchkick: Elasticsearch

## Gem hỗ trợ viết API

- doorkeeper
- grape
- jwt

## API docs

- swagger

