# BinderHub-registry
This repo contains a JSON file which characterises all of the BinderHub deployments which can run LDaCA notebooks. These definitions will be used by the LDaCA portal with a resources.yml file in the root of each registered notebook repository to filter the BinderHubs which can support that notebook repo.

The JSON is defined as follows:
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
			}
		},

        ...

    ]
}
```

Note that memory and storage values are strings with units such as M, Mi, G, or Gi. The definitions are designed to match those in the JupyterHub configuration for Binder. Anything unknown or deemed unimportant can be left as null.
