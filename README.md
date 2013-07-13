rbx-with-pry-doc-test
=====================

Stripped all of the Rails app out to make the minimal testcase.

Steps to reproduce
------------------

  1. This assumes you have RVM installed, and it's invoked to create a new minimal gemset that includes 'bundler'.
  2. run `bundle install`
     (see 'initial-gem-list.txt' for my system state)
  3. run `pry`; this starts normally for me
  4. uncomment 'pry-doc' in Gemfile
  5. run `bundle install`
     (see 'with-pry-doc-gem-list.txt')
  6. run `pry`
  
Error
-----
At step 6 above, I get an extremely long (~6k lines) 
repetitive backtrace starting with:

gem install awesome_print  # <-- highly recommended
An exception occurred running /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/bin/ruby_noexec_wrapper
    SystemStackError (SystemStackError)

Backtrace:
                                  Rubinius::Type.execute_coerce_to at kernel/common/type.rb:25
                                          Rubinius::Type.coerce_to at kernel/common/type.rb:21
                                   Rubinius::Type.coerce_to_symbol at kernel/common/type19.rb:50
                            Rubinius::Type.coerce_to_constant_name at kernel/common/type.rb:106
                                           Module(Class)#const_get at kernel/common/module19.rb:5
          { } in Marshal::State(Marshal::StringState)#const_lookup at kernel/common/marshal.rb:253
                                                        Array#each at kernel/bootstrap/array.rb:68
                 Marshal::State(Marshal::StringState)#const_lookup at kernel/common/marshal.rb:252
               Marshal::State(Marshal::StringState)#get_user_class at kernel/common/marshal.rb:675
              Marshal::State(Marshal::StringState)#construct_array at kernel/common/marshal.rb:400
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:313
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:357
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:363
  { } in Marshal::State(Marshal::StringState)#set_instance_variables at kernel/common/marshal19.rb:100
                                             Integer(Fixnum)#times at kernel/common/integer.rb:83
       Marshal::State(Marshal::StringState)#set_instance_variables at kernel/common/marshal19.rb:98
             Marshal::State(Marshal::StringState)#construct_object at kernel/common/marshal.rb:561
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:321
                              Marshal::StringState#construct_array at kernel/common/marshal.rb:410
                                             Integer(Fixnum)#times at kernel/common/integer.rb:79
              Marshal::State(Marshal::StringState)#construct_array at kernel/common/marshal.rb:409
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:313
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:357
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:363
  { } in Marshal::State(Marshal::StringState)#set_instance_variables at kernel/common/marshal19.rb:100
                                             Integer(Fixnum)#times at kernel/common/integer.rb:83
       Marshal::State(Marshal::StringState)#set_instance_variables at kernel/common/marshal19.rb:98
             Marshal::State(Marshal::StringState)#construct_object at kernel/common/marshal.rb:561
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:321
        { } in Marshal::State(Marshal::StringState)#construct_hash at kernel/common/marshal.rb:477
                                             Integer(Fixnum)#times at kernel/common/integer.rb:83
               Marshal::State(Marshal::StringState)#construct_hash at kernel/common/marshal.rb:475
                    Marshal::State(Marshal::StringState)#construct at kernel/common/marshal.rb:315
                                                      Marshal.load at kernel/common/marshal.rb:981
                  YARD::Serializers::YardocSerializer#deserialize at /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/gems/yard-0.8.6.2/lib/yard
                                                                     /serializers/yardoc_serializer.rb:77
                                     YARD::RegistryStore#[] (get) at /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/gems/yard-0.8.6.2/lib/yard
                                                                     /registry_store.rb:40
                                              YARD::Registry.root at /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/gems/yard-0.8.6.2/lib/yard
                                                                     /registry.rb:241
                                           YARD::Registry.resolve at /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/gems/yard-0.8.6.2/lib/yard
                                                                     /registry.rb:284
                                  YARD::CodeObjects::Proxy#to_obj at /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/gems/yard-0.8.6.2/lib/yard
                                                                     /code_objects/proxy.rb:228
                                   YARD::CodeObjects::Proxy#class at /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/gems/yard-0.8.6.2/lib/yard
                                                                     /code_objects/proxy.rb:145
                                YARD::CodeObjects::Proxy#kind_of? at /Users/hassan/.rvm/gems/rbx-head@pry-doc-test/gems/yard-0.8.6.2/lib/yard
                                                                     /code_objects/proxy.rb:177

