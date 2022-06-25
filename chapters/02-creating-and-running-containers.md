# Chapter 2: Creating and Running Containers

## A lousy summary

This chapter gives a review on creating and running Docker images.
It briefly touches the concept of container image format and role
of Open Container Initiative in standardization of container image
formats. It also gives a brief introduction of the overlay filesystem
which is an integral part of building container images.

The chapter also includes tips for reducing the size of the image.

## Interesting Bits

- **Overlay Filesystem**: Each layer adds, modifies or removes files
  from the preceding layer in the filesystem.
- **Container Layering**: The container image is not a single file,
  but a specification for a manifest file that points to other files.
- **Multistage Builds**: Using multistage builds, we can decrease the
  size of the application container image by not including the libraries
  and tools that are used to compile the application.

## Did I know?

- Removing a file in the subsequent layer doesn't delete the file
  from the image. The file still lives on the image, it is just
  inaccessible.
- Docker allows to put constrains on the resources used by a container.
  Following tags were discussed in this chapter:
  - `--memory`
  - `--memory-swap`
  - `--cpu-shares`
  More tags can be found in the [Docker documentations](https://docs.docker.com/engine/reference/run/#runtime-constraints-on-resources)

*Note Created: 2022-06-11*
