# Mass replacement
`perl -pi -e 's/old_string/new_string/g' file_pattern`

# Local gem development
`bundle config local.releaf ~/code/releaf`
`bundle config --delete local.releaf`

# Branch scoped database
`git config --bool branch.automatching.database true`

database.yml
```
<%
  # http://mislav.uniqpath.com/rails/branching-the-database-along-with-your-code/
  branch = `git symbolic-ref HEAD 2>/dev/null`.chomp.sub('refs/heads/', '')
  suffix = `git config --bool branch.#{branch}.database`.chomp == 'true' ? "#{branch}" : "master"
%>

development:
  adapter: mysql2
  encoding: utf8
  reconnect: false
  database: database_<%= suffix %>
  username: root
```

# Disable rails logger in console
`ActiveRecord::Base.logger = nil`
