ARG RUBY_VERSION=2.6.6
FROM ruby:${RUBY_VERSION}-alpine

# Supply AWS Recon version at build time
ARG BUNDLER_VERSION=2.1.4

# Install new Bundler version
RUN rm /usr/local/lib/ruby/gems/*/specifications/default/bundler-*.gemspec && \
    gem uninstall bundler && \
    gem install bundler -v ${BUNDLER_VERSION}

# install git
RUN apk update && apk add ca-certificates git

# Install gem (from the existing code)
COPY . /home/appuser/aws-recon
RUN cd /home/appuser/aws-recon && \
    rake install -v && \
    cp /home/appuser/aws-recon/binstub/aws_recon /usr/local/bundle/bin/ && \
    chmod +x /usr/local/bundle/bin/aws_recon

# Create non-root user
RUN adduser -D -g '' appuser

# Switch user
USER appuser
CMD ["sh"]
