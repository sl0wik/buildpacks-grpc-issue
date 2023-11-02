Issue detected on November 1, 2023.

The issue appears only on buildpack version gcr.io/buildpacks/builder:google-22 (latest) + gRPC.

To replicate:
```
git clone https://github.com/sl0wik/buildpacks-grpc-issue
cd buildpacks-grpc-issue
gcloud builds submit . --project {PROJECT} --pack image=gcr.io/{PROJECT}/grpc-test
```

Output:
```
===> DETECTING
[detector] Timer: Detector started at 2023-11-02T13:18:19Z
[detector] 6 of 8 buildpacks participating
[detector] google.php.runtime          0.0.2
[detector] google.utils.nginx          0.0.1
[detector] google.php.composer-install 0.0.1
[detector] google.php.composer         0.9.1
[detector] google.utils.label-image    0.0.2
[detector] google.php.webconfig        0.0.1
[detector] Timer: Detector ran for 226.376241ms and ended at 2023-11-02T13:18:19Z
===> RESTORING
[restorer] Timer: Restorer started at 2023-11-02T13:18:19Z
[restorer] Timer: Restorer ran for 856.495µs and ended at 2023-11-02T13:18:19Z
===> BUILDING
[builder] Timer: Builder started at 2023-11-02T13:18:20Z
[builder] === PHP - Runtime (google.php.runtime@0.0.2) ===
[builder] composer.json exists but does not specify a php version
[builder] 2023/11/02 13:18:20 [DEBUG] GET https://dl.google.com/runtimes/ubuntu2204/phpmin/version.json
[builder] ***** CACHE MISS: "phpmin"
[builder] Installing  v8.2.12.
[builder] 2023/11/02 13:18:20 [DEBUG] GET https://dl.google.com/runtimes/ubuntu2204/phpmin/phpmin-8.2.12.tar.gz
[builder] Warning: BOM table is deprecated in this buildpack api version, though it remains supported for backwards compatibility. Buildpack authors should write BOM information to <layer>.sbom.<ext>, launch.sbom.<ext>, or build.sbom.<ext>.
[builder] Warning: BOM table is deprecated in this buildpack api version, though it remains supported for backwards compatibility. Buildpack authors should write BOM information to <layer>.sbom.<ext>, launch.sbom.<ext>, or build.sbom.<ext>.
[builder] Warning: BOM table is deprecated in this buildpack api version, though it remains supported for backwards compatibility. Buildpack authors should write BOM information to <layer>.sbom.<ext>, launch.sbom.<ext>, or build.sbom.<ext>.
[builder] === Utils - Nginx (google.utils.nginx@0.0.1) ===
[builder] 2023/11/02 13:18:23 [DEBUG] GET https://dl.google.com/runtimes/ubuntu2204/nginx/version.json
[builder] ***** CACHE MISS: "nginx"
[builder] Installing Nginx Web Server v1.23.3.
[builder] 2023/11/02 13:18:23 [DEBUG] GET https://dl.google.com/runtimes/ubuntu2204/nginx/nginx-1.23.3.tar.gz
[builder] 2023/11/02 13:18:23 [DEBUG] GET https://dl.google.com/runtimes/ubuntu2204/pid1/version.json
[builder] ***** CACHE MISS: "pid1"
[builder] Installing Pid1 v1.0.8.
[builder] 2023/11/02 13:18:23 [DEBUG] GET https://dl.google.com/runtimes/ubuntu2204/pid1/pid1-1.0.8.tar.gz
[builder] Warning: BOM table is deprecated in this buildpack api version, though it remains supported for backwards compatibility. Buildpack authors should write BOM information to <layer>.sbom.<ext>, launch.sbom.<ext>, or build.sbom.<ext>.
[builder] Warning: BOM table is deprecated in this buildpack api version, though it remains supported for backwards compatibility. Buildpack authors should write BOM information to <layer>.sbom.<ext>, launch.sbom.<ext>, or build.sbom.<ext>.
[builder] Warning: BOM table is deprecated in this buildpack api version, though it remains supported for backwards compatibility. Buildpack authors should write BOM information to <layer>.sbom.<ext>, launch.sbom.<ext>, or build.sbom.<ext>.
[builder] === PHP - Composer Install (google.php.composer-install@0.0.1) ===
[builder] ***** CACHE MISS: "composer"
[builder] 2023/11/02 13:18:23 [DEBUG] GET https://getcomposer.org/installer
[builder] 2023/11/02 13:18:24 [DEBUG] GET https://composer.github.io/installer.sig
[builder] --------------------------------------------------------------------------------
[builder] failed to build: invalid composer installer found at "https://getcomposer.org/installer": checksum for composer installer, "Warning: PHP Startup: Unable to load dynamic library 'grpc.so' (tried: /layers/google.php.runtime/php/lib/php/extensions/no-debug-non-zts-20220829/grpc.so (/layers/google.php.runtime/php/lib/php/extensions/no-debug-non-zts-20220829/grpc.so: cannot open shared object file: No such file or directory), /layers/google.php.runtime/php/lib/php/extensions/no-debug-non-zts-20220829/grpc.so.so (/layers/google.php.runtime/php/lib/php/extensions/no-debug-non-zts-20220829/grpc.so.so: cannot open shared object file: No such file or directory)) in Unknown on line 0\ne21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02", does not match expected checksum of "e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02"
[builder] --------------------------------------------------------------------------------
[builder] Sorry your project couldn't be built.
[builder] Our documentation explains ways to configure Buildpacks to better recognise your project:
[builder]  -> https://cloud.google.com/docs/buildpacks/overview
[builder] If you think you've found an issue, please report it:
[builder]  -> https://github.com/GoogleCloudPlatform/buildpacks/issues/new
[builder] --------------------------------------------------------------------------------
[builder] Timer: Builder ran for 3.775596249s and ended at 2023-11-02T13:18:24Z
[builder] ERROR: failed to build: exit status 1
ERROR: failed to build: executing lifecycle. This may be the result of using an untrusted builder: failed with status code: 51
ERROR
ERROR: build step 0 "gcr.io/k8s-skaffold/pack" failed: step exited with non-zero status: 1
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
ERROR: (gcloud.builds.submit) build 068f9559-60e5-42d5-9006-ca66f69b9824 completed with status "FAILURE"
```
