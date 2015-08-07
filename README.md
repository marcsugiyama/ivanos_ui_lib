# ivanos_ui_lib
IvanOS UI is a web UI for monitoring and debugging IvanOS.

## Including in Erlang Node
1. Add ivanos_ui_lib as a rebar dependency:
```
{ivanos_ui, "", {git, "https://github.com/ivanos/ivanos_ui_lib.git", {branch, "master"}}, [raw]},
```
2. ivanos_ui_lib requires npm to compile. Add pre_hook to verify npm is installed:
```
{pre_hooks, [{'get-deps', "sh -c 'npm --version >> /dev/null || (echo \"npm not installed\"; exit 1)'"}]}.
```
3. Add a post_hook to compile ivanos_ui:
```
{post_hooks, [{'get-deps', "sh -c 'cd deps/ivanos_ui && npm install --unsafe-perm && cd -'"}]}.
```
4. Add a post_hook to copy the compiled ui into the ivanos_rest priv dir:
```
{post_hooks, [{compile, "sh -c 'cp -r deps/ivanos_ui/www deps/ivanos_rest/priv/static'"}]}.
```

## rebar.config example
```
{deps,
 [{ivanos_ui, "", {git, "https://github.com/ivanos/ivanos_ui_lib.git", {branch, "master"}}, [raw]}]
 }.

{pre_hooks, [{'get-deps', "sh -c 'npm --version >> /dev/null || (echo \"npm not installed\"; exit 1)'"}]}.

{post_hooks, [{'get-deps', "sh -c 'cd deps/ivanos_ui && npm install --unsafe-perm && cd -'"},
              {compile,
               "sh -c 'cp -r deps/ivanos_ui/www deps/ivanos_rest/priv/static'"}]}.
```
