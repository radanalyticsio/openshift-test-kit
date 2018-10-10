# openshift-test-kit

Bash tests for Openshift and Kubernetes taken from https://github.com/openshift/origin/tree/master/hack/lib
Feel free to use it, preferably as a git submodule.

## Usage

1. source the init script and setup time vars:
```bash
  source "../test/lib/init.sh"
  os::util::environment::setup_time_vars
```

2. start Kubernetes of OpenShift
3. call the assertions
```bash
  os::test::junit::declare_suite_start "operator/tests"
  os::cmd::expect_success_and_text "kubectl create -f ../manifest/operator.yaml" '"?spark-operator"? created'
  os::cmd::try_until_text "kubectl get pod -l app.kubernetes.io/name=spark-operator -o yaml" 'ready: true'
  os::test::junit::declare_suite_end
```
([example](https://github.com/radanalyticsio/spark-operator/blob/9b6a08811738e0b10b6c2dd95578fd9a33cbecf0/.travis/.travis.test-oc-and-k8s.sh#L60))

4. profit
