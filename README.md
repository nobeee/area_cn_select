[![Gem Version](https://badge.fury.io/rb/area_cn.png)](http://badge.fury.io/rb/area_cn)
## 地区选择插件(测试中) 
  整理多种地区选择器:

  1. select-ul 模拟下拉菜单(done;testing)
  2. select 下拉菜单
  3. auto complete 方式
  4. 弹出层

## Example

  [Online Demo](http://112.124.38.145:9292).

##Features
  1. 支持bootstrap  
  2. 支持simple_form

##TODO
  1. from_tag_helper district_select_ul(done)
  2. 错误处理(done)
  3. auto complete 选择器
  4. 支持x-editable **http://vitalets.github.io/x-editable/demo.html**
  5. 兼容rails 4.0
  6. 兼容ie6 

##Installation

Add it to your Gemfile:
```ruby
gem 'area_select_cn',:git=>"git@github.com:Kehao/area_select_cn.git"
```

And then execute:
```console
bundle install
```

Add it to your application.js:

```console
//= require area_select_cn/jquery.district-ul
```

if you want to use the default theme, add it to your application.css:
```console
*= require area_select_cn/district-ul
```
## AreaSelectCn::Id
### new 
```ruby
id = AreaSelectCn::Id.new("331002")  
#=> #<AreaSelectCn::Id:0x007ff87b9c4bb0 @id="331000">
# or
id = AreaSelectCn::District.id("331002")
#=> #<AreaSelectCn::Id:0x007ff87b9cbed8 @id="331002">
```

### instance methods 
```ruby
id = AreaSelectCn::Id.new("331000")  
id.name                 # => "台州市"

id.province?            # => false
id.province             # => {:text=>"浙江省",:children=>{...}}
id.province_id          # => "330000"
id.province_name        # => "浙江省"

id.city?                # => true
id.city                 # => {:text=>"台州市",:children=>{...}}
id.city_id              # => "331000"
id.city_name            # => "台州市"

id.district?                 # => false
id.district                  # => nil
id.district_id               # => nil
id.district_name             # => nil
id.area_name(default = "-")  # => "浙江省-台州市"

id.children 
#=> {"331003"=>{:text=>"黄岩区"}, "331002"=>{:text=>"椒江区"}, "331082"=>{:text=>"临海市"}...}

```
### Class methods

```ruby
AreaSelectCn::Id.select_options("331002")
# => 返回生成select需要的数据
```

## FormHelper
###form_tag
```erb
<%= form_tag "" do %>
  <%= district_select_ul(:company,:region_code,"331000") %>
<% end %>
```

###form_for
```erb
<%= form_for Company.new,:builder => AreaSelectCn::Helpers::FormBuilder do |f| %>
  <%= f.district_select_ul :region_code%>
<%end%>
```

###simple_form_for
```erb
<%= simple_form_for Company.new,:html => { :class => 'form-horizontal' } do |f| %>
  <%= f.input :region_code,:as => :district_select_ul}%>
<% end %>
```

###province,city,district select helper
```erb
<!-- form_tag -->
<%= district_select_ul(:company,:region_code,"331000") %>
<%= city_select_ul(:company,:region_code,"331000") %>
<%= province_select_ul(:company,:region_code,"331000") %>

<!-- form_for -->
<%= f.district_select_ul :region_code %>
<%= f.city_select_ul :region_code %>
<%= f.province_select_ul :region_code %>

<!-- simple_form_for -->
<%= f.input :region_code,:as => :district_select_ul %>
<%= f.input :region_code,:as => :city_select_ul %>
<%= f.input :region_code,:as => :province_select_ul %>
```

##Theme
  1. default
  2. bootstrap

if you want to use the default theme, add it to your application.css:
```console
*= require area_select_cn/district-ul
```
if you want to use bootstrap theme, you should import bootstrap css.

```erb
<!-- form_tag -->
<%= district_select_ul(:company,:region_code,"331000",:theme=>:bootstrap) %>

<!-- form_for -->
<%= f.district_select_ul :region_code,:theme=>:bootstrap,:prompt_class=>"btn btn-success"%>

<!-- simple_form_for,如果SimpleForm.wrapper等于:bootstrap，默认样式为:bootstrap -->
<%= f.input :region_code,:as => :district_select_ul %>
```
## Resources
* Chosen(http://harvesthq.github.io/chosen/)
* X-editable(http://vitalets.github.io/x-editable/demo.html)

##Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

