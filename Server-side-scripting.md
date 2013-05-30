## Warning

Custom server-side script must be consistently indented in order to function properly. This is due to Python indentation rules.

As a rule of thumb, any module-level method definition should have no indentation (i.e. not tabs before the def). For example:

    @webnotes.whitelist()
    def get_some_value():
        """A module method that fetches and returns X from the database"""

Any doc-level (class-level) method definition should be properly indented (i.e. one tab before the def). For example:

        def get_some_value(self, args=None):
            """A class method that fetches and returns X from the database"""

## Examples

Coming soon...