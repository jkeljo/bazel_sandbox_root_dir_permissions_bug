genrule(
    name="sandbox",
    cmd="stat --format '%A %U %G' / > $@",
    outs=["sandbox.txt"]
)

genrule(
    name="not_sandbox",
    cmd="stat --format '%A %U %G' / > $@",
    outs=["not_sandbox.txt"],
    tags=[
        "no-sandbox",
    ],
)

sh_test(
    name="test_perms",
    srcs=["test_perms.sh"],
    data=[
        ":sandbox",
        ":not_sandbox",
    ]
)

sh_test(
    name="test_mkdir",
    srcs=["test_mkdir.sh"],
)
