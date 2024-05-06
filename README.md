# BinderHub-registry
This repo contains a JSON file which characterises all of the BinderHub deployments known to be able to run LDaCA notebooks. These definitions will be used by the LDaCA portal together with a resources.yml file in the root of each registered notebook repository to filter the BinderHubs which can support that notebook repo.

Please refer to the [eResearch Australasia 2023 presentation](https://conference.eresearch.edu.au/wp-content/uploads/2023/11/1045-Alex-Ip.pdf) for more context.

## BinderHub registry in BinderHub-registry.json file (Server-side)
The BinderHub registry JSON is defined as follows:
```json
{
	"name": "LDaCA BinderHub Registry",
	"description": "Registry of BinderHub deployments able to be used for LDaCA-ATAP Jupyter/R notebooks",
	"url": "https://github.com/Language-Research-Technology/BinderHub-registry",
	"binderhubs": [
		{
			"name": "<display name for BinderHub deployment>",
			"description": "<long description of BinderHub deployment>",
			"url": "<root URL of BinderHub deployment>",
			"authentication": "<URL of authentication provider, or null if no authentication required: e.g. https://cilogon.org>",
			"authorisaton": "<URL of authorisation service, or null if no authorisation required: e.g. https://rems.ldaca.edu.au>",
			"resources": {
				"architecture": [
                    "<list of architectures supported, i.e. x86_64 or aarch64​. Null if unknown>"
				],
				"cpu": {
					"limit": "<maximum CPU count>",
					"guarantee": "<minimum CPU count>"
				},
				"gpu": {
					"nvidia.com/gpu": "<GPUs available>"
				},
				"memory": {
					"limit": "<maximum memory>",
					"guarantee": "<minimum memory>"
				},
				"storage": "<storage available>"
			},
			"testOnly": "<Boolean flag to indicate whether BinderHub should be omitted from live site>",
			"costPerHour": "<relative cost metric for sorting Binderhubs - could be USD$?>"
		},

        ...

    ]
}
```

Note that memory and storage values are strings with units such as M, Mi, G, or Gi. The definitions are designed to match those in the JupyterHub configuration for Binder. Anything unknown or deemed unimportant can be omitted or set as null.

## Resource specification in resources.yml file (Root directory of notebook repository)
Minimum resource requirements for the notebook(s) in a given repository should be specified in a resources.yml file in the root directory of the notebook repository. The definitions are consistent with the ```BinderHub-registry.json``` file above.

Note that the ```resources.yml``` file should be referenced in the schema.org ```availableOnDevice``` property in the associated repository RO-crate, which should conform to [this RO-crate profile](https://github.com/Language-Research-Technology/ro-crate-editor-profiles/blob/main/profiles/software-profile.json).

The ```resources.yml``` file is defined as follows:
```yaml
# resources.yml file for inclusion in the root directory of a notebook repository.
# Anything omitted is deemed to mean "don't care".
resources:
  architecture:  # Can be omitted if unimportant
  - x86_64
  - aarch64
cpu: <minimum CPU count>
gpu:
  nvidia.com/gpu:  <minimum count for specified GPU type>
memory: <minimum memory requirements>
storage: <minimum storage requirements>
```
Note that memory and storage values are strings with units such as M, Mi, G, or Gi. The definitions are designed to match those in the JupyterHub configuration for Binder. Anything unknown or deemed unimportant can be omitted or set as null.
