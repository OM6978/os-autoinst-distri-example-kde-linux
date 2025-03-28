# Example distro for openQA ![isotovideo](https://github.com/os-autoinst/os-autoinst-distri-example/workflows/isotovideo/badge.svg)

Example distro for openQA. This can be used as a template for new openQA test
projects.

To use this repository with openQA, clone this repo to
/var/lib/openqa/tests/<yourdistro>.

To use it standalone with isotovideo any other local path is fine.

When running tests based on the state in this repo the test is expected to
pass with a single needle match assuming that no bootable medium is specified
for a start.

For training purposes checkout the "training" branch which intentionally fails
as no needles are present. Creating the needles is by intention left to new
users as a learning exercise by running the test distribution within openQA
and using the openQA internal needle editor to create a new needle.

cp /home/userr/Acads/GSOC/os-autoinst-distri-example-kde-linux/hdd/kde-linux_202503220255.raw ./

openqa-cli schedule --monitor --param-file SCENARIO_DEFINITIONS_YAML=scenario-definitions.yaml $(jq -jr 'keys[] as $k | "\($k)=\(.[$k])\n"'  < vars.json)

## Communication

If you have questions, visit us on IRC in
[#opensuse-factory](irc://chat.freenode.net/opensuse-factory)


## Contribute

This project lives in
https://github.com/os-autoinst/os-autoinst-distri-example

Feel free to add issues in github or send pull requests.

### Rules for commits

* For git commit messages use the rules stated on
  [How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/)
  as a reference

If this is too much hassle for you feel free to provide incomplete pull
requests for consideration or create an issue with a code change proposal.

## Developing tests in a browser

If you only have a browser available, you can also develop tests with
[GitHub Codespaces](https://docs.github.com/en/codespaces).

On
[os-autoinst-distri-example](https://github.com/os-autoinst/os-autoinst-distri-example).
click on the "Code" button and select "Codespaces". Just click on the plus sign
to create a new Codespace. Or use
[this link](https://codespaces.new/os-autoinst/os-autoinst-distri-example?quickstart=1)
as a quickstart to resume existing instances or create new ones.

See [OpenQA in a browser](https://open.qa/docs/#_openqa_in_a_browser) for
documentation on how to use it.

You can then directly modify tests in VSCode and run
```
openqa-clone-job url-to-job CASEDIR=$PWD
```

### Local testing and CI environment

This repo is intended to be used with openQA as a learning example. The
example was first featured in the workshop talk [osc14: Ludwig Nussel, How to
write openQA tests](https://youtu.be/EM3XmaQXcLg).

One can also use the same code for running standalone isotovideo. The workflow
based on isotovideo is also used by the CI pipeline which serves as another
example how one can integrate isotovideo into a CI pipeline, here based on the
example of github actions.

Find the latest status from CI runs in
https://github.com/os-autoinst/os-autoinst-distri-example/actions

A basic CI pipeline is defined within
[.github/workflows/isotovideo.yml](.github/workflows/isotovideo.yml)
showing how isotovideo can be run against the tests. Note that this pipeline
will succeed as long as isotovideo could successfully execute the complete
test flow regardless of their individual results.

A more advanced example is shown in
[.github/workflows/isotovideo-check-all-test-modules.yml](.github/workflows/isotovideo-check-all-test-modules.yml)
which defines a pipeline that will fail if any test module returns any other
status than "ok", for example "failed".

Effectively the same workflow can be found in
[.github/workflows/isotovideo-action.yml](.github/workflows/isotovideo-action.yml),
it only uses a more GitHub action specific syntax. This makes it easier to
integrate into more complex workflows but it is less suitable for executing on
your local machine.

## License

This project is licensed under the GPL v2 license, see COPYING file for
details.
